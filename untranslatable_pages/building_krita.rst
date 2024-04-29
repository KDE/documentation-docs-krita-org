.. meta::
    :description:
        Guide to building Krita from source.

.. metadata-placeholder

    :authors: - Halla Rempt <boud@valdyas.org>
              - Wolthera van Hövell tot Westerflier <griffinvalley@gmail.com>
              - Alvin Wong
              - images and latter parts by David Revoy <info@davidrevoy.com>
    :license: GNU free documentation license 1.3 or later.
    
.. _building_krita:

==========================
Building Krita from Source
==========================

If you want to help developing Krita, you need to know how to build Krita yourself. If you merely want to run the latest version of Krita, to test a bug or play with, you can use the `nightly build for Windows <https://binary-factory.kde.org/job/Krita_Nightly_Windows_Build/>`_ the `nightly build for Linux <https://binary-factory.kde.org/job/Krita_Nightly_Appimage_Build/>`_, or the `nightly build for macOS <https://binary-factory.kde.org/job/Krita_Nightly_MacOS_Build/>`_.

.. contents::


You can build Krita on Linux, Windows, macOS and on Linux for Android. The libraries Krita needs (for instance to load and save various image types) are called dependencies.

Linux is the easiest operating system to build Krita on because all the libraries that Krita needs are available on most recent Linux distributions. For an easy guide to building Krita see `Building Krita on Linux for Cats <https://www.davidrevoy.com/article193/compil-krita-from-source-code-on-linux-for-cats>`_.

On macOS you can use tools like homebrew to get the dependencies, or build the dependencies manually. Building the dependencies manually is recommended because we have a number of changes to the source for libraries to make them function better with Krita.

On Windows you can either reuse the dependencies from the KDE Binary Factory, or build the dependencies yourself.

On all operating systems, you need to be familiar with using a terminal. Building Krita is a technical task and demands accuracy in following instructions and intelligence in understanding what happens.

Building on Linux
-----------------

In general, there are two options for building Krita on Linux. One using the docker environment (recommended) and the other is by manually building all the Krita dependencies on the host linux system (unsupported).

* :ref:`building in the Docker environment (recommended) <building_krita_with_docker>`
* :ref:`building on the host Linux (unsupported) <building_krita_on_host_linux_system>`

Building on Windows
-------------------

On Windows, you can either reuse the dependencies from the KDE Binary Factory, or build the dependencies yourself. If you decide to build all the dependencies yourself, this will take a long time. Note that you will do all your work in a CMD command window.

This is also more difficult than building Krita on Linux, so you need to pay attention to details. If you follow the guide closely, install correct dependencies and make sure your PATH doesn't contain anything unwanted, there should be no issues.

Prerequisites
~~~~~~~~~~~~~

1. Git - https://git-scm.com/downloads
2. CMake 3.16.0 or later, the latest is usually fine - https://cmake.org/download/
3. Ninja build system - https://github.com/ninja-build/ninja/releases

    - Since Ninja is a single executable, you can place it in the bin folder of CMake, next to ``cmake.exe`` for convenience.

4. LLVM MinGW compiler toolchain

    - Can be downloaded here: https://github.com/mstorsjo/llvm-mingw/releases/download/20220906/llvm-mingw-20220906-ucrt-x86_64.zip
    - Unzip the archive with `7zip <https://www.7-zip.org/>`_ into a folder like :file:`C:\\llvm-mingw`; the full path must not contain any spaces.
    - We are using the tagged release 20220906 with LLVM 15.0.0 on the Binary Factory. In theory a newer version should be compatible, but use at your own risk.
    - If you really want to use other compilers, see below.

5. You will also need a release of Python 3.10 (not 3.7, not 3.8, not 3.9, not 3.11) - https://www.python.org.

    - Make sure to have that version of python.exe in your path. This version of Python will be used for two things to configure Qt and to build the Python scripting module.  Do not set PYTHONHOME or PYTHONPATH.
    - Make sure that your Python will have the correct architecture for the version you are trying to build. If building for 32-bit target, you need the 32-bit release of Python.

6. It is useful to install Qt Creator - https://download.qt.io/official_releases/qtcreator/

.. attention::

    **Make double plus sure you do not have any other compilers or development environments or Python installation in your PATH!**


Other Compilers
^^^^^^^^^^^^^^^

- In the past we used mingw-w64 gcc 7.3.0 (mingw-builds). This version is no longer supported because our dependencies started requiring a more updated compiler to work.
- It is possible to build Krita with a newer mingw-w64 gcc toolchain, for example gcc 11.2.0 by niXman on GitHub (mingw-builds), or the one from MSYS2.
- MSYS2 can build Krita with the MINGW64, UCRT64 or CLANG64 environments.
- Krita can also be built with MSVC (check the batch file in ``build-tools\windows``). Krita built with MSVC has suboptimal performance due to codegen issues so we can't use it.

.. attention::
    
    If you use these compilers, you must build the dependencies yourself. Trying to mix dependencies built with a different compiler may outright fail to configure, or Krita may appear to build successfully but you get random crashes wuen running it.


Preparation
~~~~~~~~~~~

.. image:: /images/untranslatable/cat_guide/Krita-building_for-cats_001-init-dir_001_by-deevad.jpg

After installing the Prerequisites, prepare your working directory somewhere, like ``C:\krita-dev``. Keep this short (30 characters in the prefix path is fine, but longer than this and you may get build errors). Makes sure the path does not contain whitespace. If you use a different path, remember to adjust the paths in the later steps.

.. code:: batch

    mkdir C:\krita-dev
    cd /d C:\krita-dev

Set up python environment (you don't need to hand-craft the bat file with the predefined PATH variables):

.. code:: batch

    git clone https://invent.kde.org/dkazakov/krita-deps-management.git
    git clone https://invent.kde.org/dkazakov/ci-utilities.git -b work/split-ci-branch krita-deps-management/ci-utilities

    c:\Python310\python.exe -m venv PythonEnv --upgrade-deps
    PythonEnv\Scripts\activate.bat
    python -m pip install -r krita-deps-management\requirements.txt

Getting the dependencies
~~~~~~~~~~~~~~~~~~~~~~~~~

.. image:: /images/untranslatable/cat_guide/Krita-building_for-cats_003-get-libs_001_by-deevad.jpg

Donwload the dependencies and generate the environment file. Make sure you replace the paths to llvm-mingw and ninja:


.. code:: batch

    python krita-deps-management\tools\setup-env.py --full-krita-env -v PythonEnv -p c:\deps\llvm-mingw-20220906-ucrt-x86_64\bin\ -p c:\deps\llvm-mingw-20220906-ucrt-x86_64\x86_64-w64-mingw32\bin\ -p c:\deps\Ninja\


.. attention::
    If you happen to decide to hand-craft the ``PATH`` variable, make sure your ``PATH`` variable does **not** have double backslash symbols ``\\``. Especially as a result of multiple path variables concatenation.

    If it has, ASAN symbolizer will crash when parsing error-reports.

Every time you want to build or run your home-grown Krita, open the CMD window, change to the ``C:\krita-dev`` folder and run the ``env.bat`` file generated by the script above:

.. code:: batch

    cd /d C:\krita-dev
    env.bat

You will note that most command samples below contain these two lines, but the truth is you only need to run ``env.bat`` once for each CMD window.

Then get the source code of Krita:

.. image:: /images/untranslatable/cat_guide/Krita-building_for-cats_002-git-clone_001_by-deevad.jpg

.. code:: batch

    cd /d C:\krita-dev
    git clone https://invent.kde.org/graphics/krita.git
    
.. attention::
    If you build Krita with ASAN, make sure you don't use prebuilt deps, or at least manually rebuild Qt with
    ASAN support as well (``-DQT_ENABLE_ASAN=ON``). There is a `know issue in LLVM's linker <https://github.com/llvm/llvm-project/issues/61685>`_,
    which causes Qt be loaded before ASAN and, therefore, causing some allocations confuse ASAN. Until this issue is fixed,
    build Qt with ASAN as a workaround.

Building Krita
~~~~~~~~~~~~~~


.. image:: /images/untranslatable/cat_guide/Krita-building_for-cats_005-build_001_by-deevad.jpg



Again, on the command line, configure the build:

.. code:: batch

    cd /d C:\krita-dev
    env.bat
    mkdir -p C:\krita-dev\b_krita
    cd b_krita

    cmake C:\krita-dev\krita ^
        -DCMAKE_INSTALL_PREFIX=C:/krita-dev/_install ^
        -DBUILD_TESTING=ON ^
        -DINSTALL_BENCHMARKS=ON ^
        -DKRITA_ENABLE_PCH=OFF ^
        -DHIDE_SAFE_ASSERTS=OFF ^
        -G Ninja ^
        -DCMAKE_BUILD_TYPE=RelWithDebInfo

    ninja -j8 install
    
    
If you are hacking on Krita, you can rebuild Krita without running the full build by entering the build directory and running ``mingw32-make -j8 install`` or ``ninja -j8 install``.

.. code:: batch

    cd /d C:\krita-dev
    env.bat
    cd b_krita
    ninja -j8 install

.. image:: /images/untranslatable/cat_guide/Krita-building_for-cats_006-installing_by-deevad.jpg

    
Running Krita
~~~~~~~~~~~~~

You must start Krita from the command prompt, after having run ``env.bat``:

.. code:: batch

    cd /d C:\krita-dev
    env.bat
    _install\bin\krita
    :: or
    _install\bin\krita.exe

.. image:: /images/untranslatable/cat_guide/Krita-building_for-cats_008-running-success_by-deevad.jpg

Building on macOS
-----------------

We will build Krita on macOS with the same scripts that are used to build the nightly builds and the releases. We will *NOT* be building krita from within XCode, but from within the terminal.

Prequisites
~~~~~~~~~~~

You will need to install:

* CMake: https://cmake.org
* XCode: get it from the app store
* Qt Creator: https://download.qt.io/official_releases/qtcreator/

Preparation
~~~~~~~~~~~


Open Terminal.app

.. code:: console

    cd
    mkdir dev
    cd dev 
    git clone https://invent.kde.org/graphics/krita.git
    
.. image:: /images/untranslatable/cat_guide/Krita-building_for-cats_002-git-clone_001_by-deevad.jpg

    
Create an env.sh file that should contain the following lines:

.. code:: console

    export BUILDROOT=$HOME/dev 
    export PATH=/Applications/CMake.app/Contents/bin:$BUILDROOT/i/bin/:$PATH
    
Building the dependencies
~~~~~~~~~~~~~~~~~~~~~~~~~

.. image:: /images/untranslatable/cat_guide/Krita-building_for-cats_003-get-libs_001_by-deevad.jpg


It is possible to build Krita against dependencies installed through MacPorts or some similar packaging service. If you do that, you're on your own though.

Open Terminal.app and source the env.sh file you just created:

.. code:: console

    cd ~/dev
    . env.sh
    ./krita/packaging/macos/osxbuild.sh builddeps
    
    
This will complain several time that it cannot find the Java SDK: just click that away, and don't worry. Building the dependencies will take several hours.

Building Krita
~~~~~~~~~~~~~~

In the same terminal window (if you open a new one, you will have to *source* the env.sh script again by running ". env.sh" -- that's a dot.

.. code:: console

     ./krita/packaging/macos/osxbuild.sh buildinstall
     
This will build and install Krita to $HOME/dev/i/krita.app

.. image:: /images/untranslatable/cat_guide/Krita-building_for-cats_006-installing_by-deevad.jpg


Running Krita
~~~~~~~~~~~~~

You can run krita in the same terminal window:

.. code:: console

    ~/dev/i/krita.app/Contents/MacOS/krita
    
If you want to debug krita with lldb:

.. code:: console

    lldb ~/dev/i/krita.app/Contents/MacOS/krita
    (lldb) target create "./i/bin/krita.app/Contents/MacOS/krita"
    Current executable set to './i/bin/krita.app/Contents/MacOS/krita' (x86_64).
    (lldb) r
    
.. image:: /images/untranslatable/cat_guide/Krita-building_for-cats_008-running-success_by-deevad.jpg
    
Building on Android
-------------------

See a dedicated page for :ref:`building Krita on Android <building_krita_for_android>`


Building Krita's dependencies manually
--------------------------------------

See a dedicated page for :ref:`building Krita's dependencies manually <working_on_krita_deps>`


.. toctree::
   :maxdepth: 1
   :caption: Contents:
   :glob:

   building/*
   
