.. meta::
    :description:
        Guide to building Krita for Android

.. metadata-placeholder

    :authors:
        - Halla Rempt <boud@valdyas.org>
        - Dmitry Kazakov <dimula73@gmail.com>
    :license: GNU free documentation license 1.3 or later.
    
.. _building_krita_for_android:

==========================
Building Krita for Android
==========================

Use Linux to build Krita for Android. Building Krita for Android on another system 
is *NOT* supported yet. There are two approaches for building Krita for Android:
one with CI's docker image, and the other one straight in the host system.

.. contents::


+++++++++++++++++++++++++++
Using prebuilt docker image
+++++++++++++++++++++++++++

Docker approach is based on the normal linux-docker builds approach. You might want
to check the details in the original document for Linux: 
:ref:`Krita Docker Image <building_krita_with_docker>`

Here we expect that you have already performed all the 
:ref:`Prerequisites <building_krita_with_docker_prerequisites>` steps and 
:ref:`downloaded Krita sources <building_krita_with_docker_download_sources>` 
using the original document.

Building the Android container
------------------------------

Firstly you need to download all Krita dependencies and QtCreator. When 
fetching the dependencies you need to select he target architecture:
``x86_64``, ``armeabi-v7a`` or ``arm64-v8a``.

.. code::

    # download the dependencies and QtCreator
    ./bin/bootstrap-deps.sh --android=x86_64

    # if you don't want to fetch QtCreator, but only deps,
    # use bootstrap-krita-deps.sh
    # ./bin/bootstrap-krita-deps.sh --android=x86_64

This script will set up the full SDP environment in ``./persistent/deps`` folder. The 
deps themselves will be located in ``./persistent/deps/_install``

Now build the docker image and run the container. Just pass the ``--android`` flag to 
the ``build_image`` script and it  will fetch the correct image for you:

.. code::

    ./bin/build_image --android
    ./bin/run_container

If you are hard on harddrive space, you can cleanup the caches using the 
:ref:`cleanup section <building_krita_with_docker_cleanup>` of the original manual.

Enter the container and build Krita
-----------------------------------

.. code::

    # enter the container
    ./bin/enter

You need to manually set up a few environment variables and folders
(they might be automated later, but not right now):

.. code::

    # set ABI you are building for
    export KDECI_ANDROID_ABI=x86_64
    
    # location where _build and _packaging folders will be located
    # (don't change)
    export KDECI_WORKDIR_PATH=/home/appimage/appimage-workspace
    
    # location where the dependencies were unpacked (don't change)
    export KDECI_SHARED_INSTALL_PATH=/home/appimage/appimage-workspace/deps/usr

.. warning::

    Currently, you need to set up these variable **every time** you 
    enter the container!

Then create the build directory and enter it (don't change the location, since it
is tightly linked to ``$KDECI_WORKDIR_PATH`` in the packaging scripts)

.. code::

    mkdir -p /home/appimage/appimage-workspace/krita/_build
    cd /home/appimage/appimage-workspace/krita/_build

Configure Krita:

.. code::

    cmake -DBUILD_TYPE=RelWithDebInfo \
          -DHIDE_SAFE_ASSERTS=OFF \
          -DBUILD_TESTING=OFF \
          -DCMAKE_INSTALL_PREFIX=~/appimage-workspace/deps/usr/ \
          -DCMAKE_TOOLCHAIN_FILE=~/persistent/krita/krita-deps-management/tools/android-toolchain-krita.cmake \
          ~/persistent/krita/

There are two important switches that are unique to Android platform:

1) ``CMAKE_INSTALL_PREFIX`` is set to the same folder as the 
   dependencies themselves. It is necessary, because APK packaging
   scripts cannot search in separate directories.

2) ``CMAKE_TOOLCHAIN_FILE`` should point to a special toolchain file that will read
   custom environment variables (pre-set in the docker containter) and locates
   SDK and NDK paths.

Then build Krita as usual:

.. code::

    make -j8 install

Building the APK package
~~~~~~~~~~~~~~~~~~~~~~~~

If you set up ``KDECI_WORKDIR_PATH`` and ``KDECI_SHARED_INSTALL_PATH`` properly,
then just do:

.. code::

    python ~/persistent/krita/build-tools/ci-scripts/build-android-package.py

And you will get an APK package in ``$KDECI_WORKDIR_PATH/krita/_packaging``

If you happen to need an AAB package, then you need to generate a bit more artifacts:

.. code::

    python ~/persistent/krita/build-tools/ci-scripts/build-android-package.py --archive-artifacts
    python ~/persistent/krita/build-tools/ci-scripts/build-android-appbundle.py

The first command will build and APK and package all artifacts in 
``$KDECI_WORKDIR_PATH/krita/_packaging/krita_build_apk`` and the second script will 
reuse these artifacts for building AAB package.

++++++++++++++++++++++++++++++++++++++++++++++
Using your host system for Android development
++++++++++++++++++++++++++++++++++++++++++++++

.. warning::

    !!!This section is under a rewrite right now!!!

If you chose to build on your host system, you will have much more troubles to resolve, because
you need to set up all SDK and NDK things.

Setting up Android SDK and NDK
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

First configure prefix variable where we install our SDKs:

.. code:: shell

    export KRITA_ANDROID_ROOT=/home/appimage/appimage-workspace/android/

We right now use Android NDK version ``r22b`` to do our builds. So, it is recommended to use that. Download it from `google's
website <https://developer.android.com/ndk/downloads/older_releases.html>`__
then extract it into ``$KRITA_ANDROID_ROOT``

Next you need to download command line tools that will let you install
the SDKs and build tools. Look for links to ``commandlinetools`` at the bottom
of `android studio page <https://developer.android.com/studio>`__.
Download and extract the tools into ``$KRITA_ANDROID_ROOT``.

.. hint::
    Theoretocally, you can try installing the whole Android Studio and configure
    everything within the Studio itself, but this way is not supported currently 
    (noone just tried that).

    If you go with the Android Studio approach then open SDK manager and download 
    ``Android SDK Build-Tools`` (`more info in the official documentation 
    <https://developer.android.com/studio/intro/update#sdk-manager>`__)


Installing Prerequisites
------------------------

To build Krita for Android you need to have **a specific version** of Java 
installed on your machine:

.. code:: shell

    sudo add-apt-repository ppa:openjdk-r/ppa
    sudo apt-get update
    sudo apt-get install openjdk-17-jdk # exactly this version!

Check if no other version of Java is installed. If installed, either remove it 
(recommended) or make sure Ubuntu's ``update-alternatives`` pulls exactly version 17 
for ``javac`` **and the runtime** (no idea how to check that).

.. code:: shell

    # make sure both commands link to version 17!
    javac --version
    ls -l /usr/lib/jvm/*

Install SDKs and build tools:

.. code:: shell

    cd $KRITA_ANDROID_ROOT
    cmdline-tools/bin/sdkmanager --sdk_root=$KRITA_ANDROID_ROOT/sdk/ --licenses
    cmdline-tools/bin/sdkmanager --sdk_root=$KRITA_ANDROID_ROOT/sdk/ platform-tools
    cmdline-tools/bin/sdkmanager --sdk_root=$KRITA_ANDROID_ROOT/sdk/ "platforms;android-23" # TODO:not needed?
    cmdline-tools/bin/sdkmanager --sdk_root=$KRITA_ANDROID_ROOT/sdk/ "platforms;android-33"
    cmdline-tools/bin/sdkmanager --sdk_root=$KRITA_ANDROID_ROOT/sdk/ "build-tools;34.0.0"

.. hint::

    Krita's current minimal API-level is ``android-23``. We can theoretically 
    install the latest avalable SDK and NDK that still supports this API-level. Though
    we update not that often, so our versions may drag a little behind.

    The backwards compatibility of NDK and SDK can be checked here:

    * NDK: https://developer.android.com/ndk/downloads/revision_history
    * SDK: ``where???``

Adjust ``PATH`` variable to use the installed android tools:

.. code:: shell

    export PATH=$KRITA_ANDROID_ROOT/sdk/emulator/:$PATH
    export PATH=$KRITA_ANDROID_ROOT/sdk/platform-tools/:$PATH
    export PATH=$KRITA_ANDROID_ROOT/cmdline-tools/bin/:$PATH


Building Krita's deps
---------------------

First you need to set up environment variables that are used by our ``androidbuild.sh`` 
script:

.. code:: shell

    export KRITA_ROOT=/home/appimage/persistent/krita/
    export BUILD_ROOT=/home/appimage/appimage-workspace/krita-build/
    export ANDROID_ABI=x86_64
    export ANDROID_API_LEVEL=23
    export CMAKE_ANDROID_NDK=$KRITA_ANDROID_ROOT/android-ndk-r22b/
    export ANDROID_SDK_ROOT=$KRITA_ANDROID_ROOT/sdk/
    export BUILD_TYPE=Release

You can modify ``ANDROID_ABI`` and ``BUILD_TYPE`` if you want to build for another 
architecture:

* ``ANDROID_ABI``: x86_64, armeabi-v7a, arm64-v8a
* ``BUILD_TYPE``: Release, Debug

.. warning::

    Please take it into account that 32-bit x86 versions of Krita are now deprecated 
    and not officially supported.

Now build the dependencies (the script will fetch all the options from
the environment variables we set before):

.. code:: shell

    $KRITA_ROOT/packaging/android/androidbuild.sh -p=boost
    $KRITA_ROOT/packaging/android/androidbuild.sh -p=qt
    $KRITA_ROOT/packaging/android/androidbuild.sh -p=3rdparty
    $KRITA_ROOT/packaging/android/androidbuild.sh -p=kf5

Build Krita and the APK file:

.. code:: shell

    $KRITA_ROOT/packaging/android/androidbuild.sh -p=krita-bin
    $KRITA_ROOT/packaging/android/androidbuild.sh -p=apk

The APK package will be placed into ``$BUILD_ROOT/krita_build_apk/build/outputs/apk/{debug,release}`` 
folder.

Installing Android Emulator
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Using Android emulator is easy, after it is configured initially. The only issue 
that worth remembering is that when using x86_64 builds the host system should 
support KVM virtualization. KVM virtualization is not required for emulating ARM 
target.

.. warning::

    [TODO] Krita docker does not automatically add 'kvm' group into the client system (yet),
    it should be done manually:

    1) Add kvm group into the docker **with the same group-id as on the host machine**
    2) Add appimage user into kvm group
    3) Relogin into the appimage user for the changes to take effect

Install cpu-checker and check if KVM is supported on your system (or in the 
docker container):

.. code:: shell

    sudo apt-get install cpu-checker
    # Check if kvm is available
    kvm-ok

Install the system image for the target system. Change ``x86_64`` to the target 
architecture you would like to test:

.. code:: shell

    sdkmanager --sdk_root=$KRITA_ANDROID_ROOT/sdk/ "system-images;android-23;google_apis;x86_64"

Create the virtual device:

.. code:: shell

    # save the device name
    export device_name=Test_API_23

    # create the device
    avdmanager create avd --force --name $device_name --abi x86_64 --package 'system-images;android-23;google_apis;x86_64'

    # create an SD card for the device
    mksdcard -l testsdcard 512M $KRITA_ANDROID_ROOT/sdcard.img

Open configuration file for the new device (located at ``~/.android/avd/Test_API_23.avd/config.ini``)
and edit the following values:

.. code:: ini

    # increase cache size
    disk.cachePartition.size=512MB
    
    # increase the size of the root partition
    disk.dataPartition.size=3000M

    # if using x86_64 or arm64-v8a targets, enable GPU acceleration
    hw.gpu.enabled=yes
    hw.gpu.mode=auto

    # make sure that the screen size is not too tiny
    hw.lcd.density=180
    hw.lcd.depth=16
    hw.lcd.height=1080
    hw.lcd.vsync=60
    hw.lcd.width=1920

    # increase the amount of RAM available for the device
    hw.ramSize=4096M

    # set up teh SD card
    sdcard.size=512 MB
    sdcard.path=<path to your sd card>/sdcard.img

    # increase the size of VM heap
    vm.heapSize=1024M

Run the emulator (add ``-wipe-data`` switch if you would like to reset the device):

.. code:: shell

    emulator -avd $device_name -no-snapshot -no-boot-anim

Install Krita on the device:

.. code:: shell

    adb install ./krita-x86_64-5.2.0-prealpha-debug.apk

When the container it not needed anymore, it can be removed with the follwoing command:

.. code:: shell

    avdmanager delete avd -n $device_name


Debugging crashes
~~~~~~~~~~~~~~~~~

If Krita crashes you can look up the logs using ``adb logcat``
