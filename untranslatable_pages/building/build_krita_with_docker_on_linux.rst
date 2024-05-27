.. meta::
    :description:
        Guide to building Krita with docker on Linux.

.. metadata-placeholder

    :authors: - Halla Rempt <boud@valdyas.org>
    :license: GNU free documentation license 1.3 or later.
    
.. _building_krita_with_docker:

===================================
Building krita with Docker on Linux
===================================

This guide is useful when you are an advanced developer and want to build krita with the same patched dependencies that are used for the AppImages. If you just want to hack on Krita, read the Build Krita from Source guide.

The *Dockerfile* is based on the official KDE build environment
that is used on KDE CI for building official AppImage packages. This guide is valid for Ubuntu and Ubuntu-based Linux distributions.

.. contents::

.. _building_krita_with_docker_prerequisites:

Prerequisites
-------------

First make sure you have Docker installed

.. code::

    sudo apt install docker docker.io

Decide where you want to store your Docker images. All the docker images and containers are by default stored in a special docker-daemon controlled folder under */var* directory. You might not have enough space there for building Krita (it needs about 10 GiB). In such a case it is recommended to move the docker images
folder into another location, where there is enough space.

1) Stop docker service

    .. code::

        sudo systemctl stop docker

2) Edit the config file:

    On newer systems, like Ubuntu 18.04 and higher you need to open file */etc/docker/daemon.json* and add the following json config options:

    .. code::

        {
            "data-root" : "/path/where/you/want/to/store/docker/images/"
        }

    If you have older version of Ubuntu, e.g. Ubuntu 16.04, then you need to do the following:

    .. code::
    
        echo 'DOCKER_OPTS="-g /path/where/you/want/to/store/docker/images/"' >> /etc/default/docker

3) Restart the docker service

    .. code::

        sudo systemctl start docker

Second, make sure that you have python3 and python3-venv packages installed:

.. code::

    sudo apt install python3 python3-venv

``python3-venv`` package is used for bootstrapping the dependencies on the host system before 
building the docker image, so you need to have it preinstalled.


.. _building_krita_with_docker_download_sources:

Downloading Krita sources
-------------------------

Then you need to download deps and Krita source tree. These steps are not included into the *Dockerfile* to save internal bandwidth 

.. code::

    # create directory structure for container control directory
    git clone https://invent.kde.org/dkazakov/krita-docker-env krita-auto-1

    cd krita-auto-1
    mkdir persistent

    # copy/checkout Krita sources to 'persistent/krita'
    cp -r /path/to/sources/krita ./persistent/krita

    ## or ...
    # git clone kde:krita persistent/krita
    # "kde:krita" should be replaced with a link for cloning the repository,
    # such as "git@invent.kde.org:graphics/krita.git".


Downloading prebuilt Krita dependencies
---------------------------------------

.. code::
    
    # download the deps archive
    ./bin/bootstrap-deps.sh

.. note::

    If you want to build and ASAN-capable build of Krita, then you should make sure that this
    script installs an ASAN-capable version of Qt. To do that, declare an environment variable
    on your host **before** bootstrapping the deps:

    .. code:: bash

        export KDECI_PACKAGE_ALIASES_YAML='{ ext_qt : ext_qt-asan }'

    If you don't want ASAN-capable, but just a debug-capable build of Qt, then
    change this variable to:

    .. code:: bash

        export KDECI_PACKAGE_ALIASES_YAML='{ ext_qt : ext_qt-debug }'

Build the docker image and run the container
--------------------------------------------

.. code::

    ./bin/build_image
    ./bin/run_container

.. _building_krita_with_docker_cleanup:

Cleanup the dependencies
------------------------

The dependencies are cached in ``~/persistent/deps/`` folder. It may occupy
up to 4.7 GiB. If you happen to have problems with space, make sure you
removed all the cached checkout:

.. code::

    # clean up about 2.4 GiB of the cached deps checkout

    rm -rf ./persistent/deps/_install

If you need more space, you can freely remove the entire deps cache
(it will be automatically refetched on the next call to ``./bin/bootstrap-deps.sh``)

.. code::

    # clean up everything

    rm -rf ./persistent/deps/


Enter the container and build Krita
-----------------------------------

.. code::

    # enter the docker container (the name will be
    # fetched automatically from '.container_name' file)

    ./bin/enter

... now you are inside the container with all the deps prepared ...

.. code::

    # build Krita as usual
    # you should be in ~/appimage-workspace/krita-build/
    ~/bin/run_cmake.sh ~/persistent/krita
    make -j8 install

    # start Krita
    ../krita.appdir/usr/bin/krita

.. note::

    If you need to build an ASAN-capable build of Krita (**and** you have passed
    ``KDECI_PACKAGE_ALIASES_YAML`` during the dependencies fetch phase), then pass
    ``-DECM_ENABLE_SANITIZERS=address`` to CMake as well.

Building AppImage package for your version of Krita
---------------------------------------------------

If you want to build a portable package for your version of Krita, just enter
the container and type:

.. code::

    ~/bin/build_krita_appimage.sh

The built package will be copied to *./persistent/* folder.

By default, the package will be built in release mode. If you want to
add debugging information, add *--debug* option to the command line:

.. code::

    ~/bin/build_krita_appimage.sh --debug

Creating a full clone of the container
--------------------------------------

It is possible to copy the container with the entire environment, sources,
build directory and QtCreator installation and configuration. After cloning,
no rebuild of Krita is needed!

To copy container to *../krita-auto-2*, just type in the host system

.. code::

    ./bin/spawn-clone -d ../krita-auto-2

*spawn-clone* will make an image from the current container and create a
new one out of it. This image will be cached for further usages. If you need
to flush the cache, pass *-f* option to *spawn-clone*:

.. code::

    ./bin/spawn-clone -f -d ../krita-auto-2

You can start several instances of *spawn-clone* on the same container
concurrently (e.g. for building multiple merge requests). It has internal
locking mechanism for resolving concurrency problems    

Testing merge requests using container clones
---------------------------------------------

To quickly build a merge request '123' basing on the current state of the
container type in the host system

.. code::

    ./bin/spawn-clone -m 123 -be

The script will clone the container, checkout the merge request branch,
build it and provide you a terminal for running Krita. The container
will be created at *./clones/clone-mr-123* subfolder of the current container.

If you also want to build an AppImage, add *--release-appimage* option:

.. code::

    ./bin/spawn-clone -m 123 --release-appimage -be

AppImage will be places at *./persistent* subfolder of the clone.
When finished with testing the merge request, you can remove the clone
completely by running

.. code::

    ./bin/discard-clone /clones/clone-mr-123

You can build multiple merge requests at once!


Updating dependencies in the docker
-----------------------------------

Sometimes dependencies in Krita change and building Krita or making the AppImage fails. To fix that, you need to update the dependencies.

.. note::

    This method is slow, because you need to rebuild the whole docker, which includes rebuilding whole Krita.

Run those commands in the console in the host system. If you want to update the dependencies in a clone docker, just go to the clone directory where you see ``bin`` and ``persistent`` directories and run those commands there.

.. code::

    # remove old dependencies
    rm ./persistent/deps/_install

    # download new deps
    ./bin/bootstrap-deps.sh

    # remove the current container
    ./bin/remove_container

    # remove the image for the current container
    docker image remove krita-auto-1

    # build image
    ./bin/build_image

    # run the container (it will create one)
    ./bin/run_container

After that you need to build Krita in the docker as usual.

.. note::

    Don't forget about setting ``KDECI_PACKAGE_ALIASES_YAML`` if you need any special flavour
    of the Qt library installed.


Extra developer tools
---------------------

QtCreator is usually installed into the docker image into ``~/qtcreator/`` folder. The fetching of the prebuilt QtCreator 
happens when you run ``./bin/bootstrap-deps.sh`` script. That is, if you skipped installing deps QtCreator will not be installed
and you will have to download it manually from `this location <https://files.kde.org/krita/build/qtcreator-package.tar.gz>`_.

You may also try to dowload the official QtCreator installer from `<https://download.qt.io/official_releases/qtcreator/>`_. In 
case you decide to use it, just enter the container and install it. Make sure you install it into '~/qtcreator' directory without 
any version suffixes, then you will be able to run it directly from the host system using the script below:

.. code::

    # from the host
    ./bin/qtcreator


Stopping the container and cleaning up
--------------------------------------

When not in use you can stop the container. All your filesystem state is saved, but all the currently running processes are killed (just ensure you logout from all the terminals before stopping).

.. code::

    # stop the container
    ./bin/stop

    # start the container
    ./bin/start


If you don't need your container/image anymore, you can delete them from the docker

.. code::

    # remove the container
    sudo docker rm krita-auto-1

    # remove the image
    sudo docker rmi krita-deps


Troubleshooting
---------------

Krita binary is not found after the first build
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Either relogin to the container or just execute `source ~/.devenv.inc`

OpenGL doesn't work on NVidia GPU with proprietary drivers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The docker run script automatically forwards the GPU devices into the container, but it doesn't install the drivers for the GPU. You should install exactly the same version of the driver that is installed on your host system. Just run the following script when you are on host:

.. code::

    ./bin/install_nvidia_drivers.sh

