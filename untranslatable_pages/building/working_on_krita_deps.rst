.. meta::
    :description:
        Working on Krita dependencies

.. metadata-placeholder

    :authors: - Dmitry Kazakov <dimula73@gmail.com>
    :license: GNU free documentation license 1.3 or later.
    
.. _working_on_krita_deps:

=============================
Working on Krita Dependencies
=============================

Sometimes it happens that you need to patch/fix some of Krita dependencies. In this 
case you have to build your own version of the dependency instead of using the prebuilt
package.

This manual describes the build process for the Linux host system using the docker environment. The process 
of building deps on Windows, MacOS and Android is almost the same. If the command differs on other systems, you
will see a note about that inline. If you are not familiar with the docker-based build process, please 
check the docker environment manual: :ref:`Building Krita with Docker on Linux <building_krita_with_docker>`

.. warning::

    Buillding the Linux deps on the host system without the docker environment 
    is **not supported** and is not going to be supported. It is almost impossible
    to do.
    
    Building the Android deps on the host system without using docker is possible,
    but still **not supported**. You will need to consult `the Dockerfile for Kirta's Android 
    builder image <https://invent.kde.org/sysadmin/ci-images/-/blob/master/krita-android-builder/Dockerfile>`_ 
    to set up proper versions of the deps.

.. contents::

.. _building_deps_prerequisites:

Building and modifying a single dependency
==========================================

Prerequisites
-------------

The manual expects that you do already have a working docker environment with the 
prebuild deps installed. See :ref:`Building Krita with Docker <building_krita_with_docker>`
for details.

.. _deps_setting_up_folders:

Setting up folders
------------------

First you need to set up folders structure, initialize Python's 
virtual environment and install python modules into that:


.. code:: bash

    mkdir /home/appimage/appimage-workspace/root
    cd /home/appimage/appimage-workspace/root
    git clone https://invent.kde.org/dkazakov/krita-deps-management.git
    git clone https://invent.kde.org/dkazakov/ci-utilities.git krita-deps-management/ci-utilities
    python3 -m venv PythonEnv
    source ./PythonEnv/bin/activate
    pip install -r krita-deps-management/requirements.txt

If you used prebuilt deps, you might want to reuse the packages cache from the host system. 
Just create a symlink for it:

.. code:: bash

    ln -s ~/persistent/deps/cache /home/appimage/appimage-workspace/root/cache


Setting up the environement
---------------------------

Now you need to create the development environment:

.. code:: bash

    python krita-deps-management/tools/setup-env.py -r ./ -v PythonEnv/ -s /home/appimage/appimage-workspace/deps/usr

This line sets the environment scripts in the current folder
(``-r ./``) and configures the "shared install folder" to coincide
with the folder where prebuilt deps are preinstalled by the 
container initialization scripts
(``-s /home/appimage/appimage-workspace/deps/usr``)


.. note::

    If you are setting up the Android environment, pass ``--android-abi <targe-arg>`` option to this
    script (where ``<target-arg>`` is one of ``x86_64``, ``armeabi-v7a`` or ``arm64-v8a``)

The script has generated an environment file for you. Just source it now:

.. code:: bash

    source /home/appimage/appimage-workspace/root/base-env

Next time you enter the docker container, just repeat this "source" line and it will
activate the environment for you.

If you are developing for Android or MacOS, you should also set up the toolchain file for
the build:

.. code:: bash

    # for Android
    export KDECI_EXTRA_CMAKE_ARGS="-DCMAKE_TOOLCHAIN_FILE=/home/appimage/appimage-workspace/root/krita-deps-management/tools/android-toolchain.cmake"

    # for MacOS
    export KDECI_EXTRA_CMAKE_ARGS="-DCMAKE_TOOLCHAIN_FILE=/home/appimage/appimage-workspace/root/krita-deps-management/tools/macos-toolchain.cmake"

You should manually set this variable every time you enter the container. It is neceesary because the toolchain file 
for building Krita itself differs. If you need to build Krita in the same environment, you should
change the toolchain file name to the one with "-krita" suffix, i.e. ``android-toolchain-krita.cmake``


Building the dependency
-----------------------

To build a single dependency, just enter its subfolder and issue the build command:

.. code:: bash

    cd krita-deps-management/ext_qt/
    python -u ../ci-utilities/run-ci-build.py --project ext_qt --branch master --platform Linux -e env --skip-dependencies-fetch

Make sure you change the "project" and "platform" arguments of the command. You can try replacing 
``--project ext_qt`` with ``--project $(basename $(pwd))`` if you are on Linux.

The possible strings for "platform" option are:

* ``Linux``
* ``Windows``
* ``MacOS``
* ``Android/x86_64``
* ``Android/armeabi-v7a``
* ``Android/arm64-v8a``

The script will (hopefully) build the dependency for you and leave you two files in the dependency subfolder:

* ``krita-deps-management/ext_qt/env``
* ``krita-deps-management/ext_qt/env_deactivate``

You can source the first file to activate environment for building **this very subproject**. When switching 
to another subproject, don't forget to deactivate the environment with the second 
script.

.. note::

    Sourcing ``env`` and ``base-env`` scripts will also set up two special variables for you that will help
    you determine which environment you are in:

    * ``KDECI_ENV_ACTIVATION_SCRIPT``
    * ``KDECI_ENV_DEACTIVATION_SCRIPT``

    Hence, to deactivate the current environement you can just call:

    .. code:: bash

        source $KDECI_ENV_DEACTIVATION_SCRIPT

After the project is built at least once, you can edit its sources 
and do incremental rebuilds manually :

.. code:: bash

    cd krita-deps-management/ext_qt
    
    # activate the environment
    source ./env

    # go to the sources directory
    pushd _build/ext_qt-prefix/src/ext_qt

    ## ... patch the sources as much as you need ...

    # go to the build directory
    popd
    pushd _build/ext_qt-prefix/src/ext_qt-build

    # build and install the project as usual
    make -j8 install

    # on Windows and MacOS you might need to use 
    # Ninja instead:
    ## ninja -j8 install

    # after the work is done, deactivate the per-project environment
    source ./env_deactivate

    # alternatively, use the environment variable for that
    # source $KDECI_ENV_DEACTIVATION_SCRIPT

Building all packages in isolated environments
==============================================

When testing dependency build scripts you might need to test if each package can be built 
independently in an isolated encironment. In such a case, the "shared install folder"
method will not work. Instead, you needs to use "publish to cache" method. With 
this method, each subproject is built in an isolated environment, with only 
minimally necessary depenencies present. Each subproject is then packaged and 
"uploaded" into the package cache. By the end of the build process the local cache
is "forcefully" populated with the locally built packages, which are newer than 
the ones in the registry. These local packages will later be used for building Krita 
itself.

This method works almost the same as the previous one, with a few minor differences.

Firstly, you need to skip installing the prebuilt dependencies when building 
the docker image. To do that, pass ``-s`` (or ``--skip-deps``) option to ``build_image`` 
script:

.. code:: bash

    ./bin/build-image -s

This will create a container image without any prebuilt deps installed.

Then run the container and follow the folders setup process as described above 
in :ref:`Setting up folders <deps_setting_up_folders>` section.

When folders are set up, generate the envidonment **without** the ``-s`` option.
It will disable the "shared install feature":

.. code:: bash

    python krita-deps-management/tools/setup-env.py -r ./ -v PythonEnv/
    source /home/appimage/appimage-workspace/root/base-env

.. note::

    If you are setting up the Android environment, don't forget to pass ``--android-abi <targe-arg>`` option to the
    script (where ``<target-arg>`` is one of ``x86_64``, ``armeabi-v7a`` or ``arm64-v8a``)


Set up ``KDECI_EXTRA_CMAKE_ARGS`` if you are on MacOS or Android.

Make sure your pacakges cache is clean:

.. code:: bash

    rm -rf /home/appimage/appimage-workspace/root/cache/*.{tar,json}

Run the build of all the packages:

.. code:: bash

    cd krita-deps-management
    python -u ../ci-utilities/seed-package-registry.py --platform Linux --seed-file latest/krita-deps.yml --publish-to-cache --missing-only

If some build has failed, fix it and then just rerun this command. Thanks to ``--missing-only`` the script 
will skip the subprojects that has been successfully built.

When the build process fails, you can manually rebuild the failing project by running
``run-ci-build.py`` script manually in the corresponding folder.

