f.. meta::
    :description:
        Releasing Krita

.. metadata-placeholder

    :authors: - Dmitry Kazakov <dimula73@gmail.com>
    :license: GNU free documentation license 1.3 or later.

.. _release_krita:

==========================
Making a release
==========================

.. contents::

Krita releases and update channels
----------------------------------

At any point of time Krita users have access to four(!) versions of Krita. We calls these versions "channels", since they are "channels through which the users can get updates of the software".

1. **Krita Stable** is the latest stable version of Krita that has been released to the users
    
    * the user can manually download it from the official side

    * packages are stored at the "stable" prefix on dko: https://download.kde.org/stable/krita/

    * AppImage updater will suggest an update **only** from one stable version to another, e.g. "Krita 5.2.2 -> Krita 5.2.3" or "Krita 5.2.2 -> Krita 5.3.0"

    * AppImage updater uses link at address: https://download.kde.org/stable/krita/updates/Krita-Stable-x86_64.appimage.zsync

2. **Krita Beta** is the latest alpha or beta version of Krita

    * these packages are supposed to be used for pre-release testing

    * we usually make beta-release announcements with direct links to these packages

    * packages are stored at the "unstable" prefix on dko: https://download.kde.org/unstable/krita/

    * AppImage updater will suggest updates if

        * the next beta or release candidate version has been released;

        * the final release is published (update to final)

    * AppImage updater uses link at address: https://download.kde.org/unstable/krita/updates/Krita-Beta-x86_64.appimage.zsync

3. **Krita Plus** is the latest stable release with all backported patches, built nightly

    * this channel is basically the nightly build of the current stable branch

    * packages are stored at the gitlab's CDN server: https://cdn.kde.org/ci-builds/graphics/krita/krita-5.2/

    * AppImage updater will suggest updates if

        * a new nightly with the same minor version has been published, e.g.

            + krita/5.2 will update to the new version of krita/5.2

            + krita/5.3 will update to the new version of krita/5.3

            + they will not cross-update, unless the next point...

        * a stable version of the next minor branch has been officially released

            + krita/5.2 will update to krita/5.3 **after** the first official stable release of krita/5.3 has been made

    * AppImage updater uses link at the corresponding branch at CDN:

        - krita/5.2 packages use: https://cdn.kde.org/ci-builds/graphics/krita/krita-5.2/linux/Krita-Plus-x86_64.appimage.zsync

        - krita/5.3 packages use: https://cdn.kde.org/ci-builds/graphics/krita/krita-5.3/linux/Krita-Plus-x86_64.appimage.zsync

        - after the first version of krita/5.3 has been released, the link in 5.2 branch should be replaced

    * **TODO:** remap these links to some static location at https://updates.krita.org/krita-5.2/linux/Krita-Plus-x86_64.appimage.zsync

4. **Krita Next** is the nightly build of the development (``master``) branch of Krita

    * packages are stored at the gitlab's CDN server: https://cdn.kde.org/ci-builds/graphics/krita/master/

    * AppImage updater will suggest updates every time development branch gets a new nightly build

    * AppImage updater uses link at address: https://cdn.kde.org/ci-builds/graphics/krita/master/linux/Krita-Next-x86_64.appimage.zsync

    * **TODO:** remap these links to some static location at https://updates.krita.org/master/linux/Krita-Next-x86_64.appimage.zsync

On branching out a stable branch
--------------------------------

When we change the stable branch name, e.g. when changing `krita/5.2` into `krita/5.3` we should update its name in several
places to keep CI infrastructure working properly:

1. APK signer: https://invent.kde.org/sysadmin/ci-utilities/-/blob/master/signing/apksigner-projects.yaml

2. Windows signer: https://invent.kde.org/sysadmin/ci-utilities/-/blob/master/signing/windowsbinariessigner-projects.yaml

3. Nightly builds publisher: https://invent.kde.org/sysadmin/ci-utilities/-/blob/master/signing/buildpublisher-projects.yaml

4. Translations' "stable" branch: https://invent.kde.org/sysadmin/repo-metadata/-/blob/master/projects-invent/graphics/krita/i18n.json

5. Notify translators about the tranlsations branch switch!

6. Update the link to "Krita Plus" ZSync channel in ``build-tools/ci-scripts/show-updates-status.py`` script

    * make sure you keep the old link in the script as well, until the branch is fully deprecated and removed 
      from the CDN server (we need to keep the link up for some time to let people update to the new version)

7. Update Krita version in ``master`` branch to be higher than in stable.


Before the release
------------------

1. Coordinate with #kde-promo
2. Notify translators of string freeze!
3. Verify that the release notes page is done, like https://krita.org/en/krita-4-2-release-notes/
4. Verify that all dependency builds are up to date. Remember that these builds are built from **master**, not from the stable branch.

    * https://binary-factory.kde.org/job/Krita_Android_arm64-v8a_Dependency_Build/
    * https://binary-factory.kde.org/job/Krita_Android_armeabi-v7a_Dependency_Build/
    * https://binary-factory.kde.org/job/Krita_Android_x86_64_Dependency_Build/
    * https://binary-factory.kde.org/job/Krita_Android_x86_Dependency_Build/
    * https://binary-factory.kde.org/job/Krita_Nightly_Appimage_Dependency_Build/
    * https://binary-factory.kde.org/job/Krita_Nightly_MacOS_Dependency_Build/
    * https://binary-factory.kde.org/job/Krita_Nightly_Windows_Dependency_Build/
    
    Compare the build date and included commits to the commit in 3rdparty directory in master:
    
    .. code::
    
        git fetch origin && git log origin/master 3rdparty
    

Update version in source code
-----------------------------

1. !! REMOVE THE SURVEY LINK !! (or, if this is a beta, make a survey and update the survey link)
2. update the version of krita5.xmlgui
3. update the CMakeLists.txt version
4. update the snapcraft.yaml file
5. update the appstream screenshots: https://invent.kde.org/websites/product-screenshots
6. update org.kde.krita.appdata.xml 's release tag in the BRANCH
7. update download_release_artifacts.sh
8. update Android version (keep in mind that *all* Krita releases on Android are marked as Beta at the moment): packaging/android/apk/build.gradle
9. When releasing beta-version double-check that you updated to "beta1", not just plain "beta". Only "alpha" versions can be made without a number, because they are built nightly.

Update versions in the stable branch to avoid XMLGUI conflicts
--------------------------------------------------------------
1. stable branch is always marked as "alpha" (without a number in the end)
2. update the version of krita.xmlgui; it should be `$(( $VERSION_IN_RELEASE_BRANCH + 1 ))`
3. update the CMakeLists.txt version
4. update org.kde.krita.appdata.xml 's release tag
5. packaging/android/apk/AndroidManifest.xml 

Create the tarball
------------------

Create and push the tag
~~~~~~~~~~~~~~~~~~~~~~~

1. Set the tag: 

    .. code::
    
        git tag -a v5.1.0-beta1 -m "Krita 5.1.0 Beta1"

2. Push the tag: 

    .. code::
    
        git push origin refs/tags/v5.1.0-beta1:refs/tags/v5.1.0-beta1

3. If you need to change the tag position (not recommended):

    .. code::

        # remove the previous tag

        git push origin :refs/tags/v5.1.0-beta1

        # make a new tag locally
        git tag -a v5.1.0-beta1 -m "Krita 5.1.0 Beta1"

        # push the new tag
        git push origin refs/tags/v5.1.0-beta1:refs/tags/v5.1.0-beta1

        # all Krita developers now have to refetch tags to 
        # get the updated tag position
        git fetch origin --tags

Create the tarball
~~~~~~~~~~~~~~~~~~

1. Get the tarball from gitlab: https://invent.kde.org/graphics/krita/-/tags
2. Unpack the tarball
3. Rename folder from `krita-v5.1.0-beta1` into `krita-5.1.0-beta1` (without 'v' prefix in the version string)
4. Package the tarball as .gz and .xz
5. Sign both tarballs:

    .. code::

        gpg --output krita-5.1.0-beta1.tar.gz.sig --detach-sign krita-5.1.0-beta1.tar.gz
        gpg --output krita-5.1.0-beta1.tar.xz.sig --detach-sign krita-5.1.0-beta1.tar.xz

6. Upload the gz tarball to files.kde.org, where builders can pick them up (the sigs and the xz tarball aren't used for the binary builders):

    * https://files.kde.org/krita/.release/$version/krita-$version.tar.gz


Make Windows, Linux, macOS and Android packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

8. Request four release builds on binary-factory.kde.org, after starting each build,go to "Console Output" section, click on "Input Requested" and choose a tarball version to build.

    * https://binary-factory.kde.org/job/Krita_Release_Windows64_Build/
    * https://binary-factory.kde.org/job/Krita_Release_Appimage_Build/
    * https://binary-factory.kde.org/job/Krita_Release_MacOS_Build/
    * https://binary-factory.kde.org/job/Krita_Release_Android_arm64-v8a_Build/
    * https://binary-factory.kde.org/job/Krita_Release_Android_armeabi-v7a_Build/
    * https://binary-factory.kde.org/job/Krita_Release_Android_x86_64_Build/
    * https://binary-factory.kde.org/job/Krita_Release_Android_x86_Build/

Runs

    * https://binary-factory.kde.org/job/Krita_Release_Android_AppBundle_Build/ (after the android builds are done)

9. Download all built artifacts using `download_release_artifacts.sh` script. Open the script and modify `KRITA_VERSION` variable to correspond to the version string.

10. For each build check:

    * Krita starts
    * Localization works
    * Python plugins are available
    * Basic painting and most recently fixed bugs are fixed

11. Sign the AppImage:

    .. code::

        gpg --detach-sign --output krita-5.1.0-beta-x86_64.appimage.sig krita-5.1.0-beta-x86_64.appimage


12. Sign four Android packages (or send them to Halla for signing)

    Note: there is a useful script for signing them...

    * krita-arm64-5.1.0-beta1-unsigned.apk
    * krita-arm32-5.1.0-beta1-unsigned.apk
    * krita-x86-5.1.0-beta1-unsigned.apk
    * krita-x86_64-5.1.0-beta1-unsigned.apk

    After signing, remove "-unsigned" suffix, so the signed packages would look like that:

    * krita-arm64-5.1.0-beta1.apk
    * krita-arm32-5.1.0-beta1.apk
    * krita-x86-5.1.0-beta1.apk
    * krita-x86_64-5.1.0-beta1.apk

13. Now you should have 18 files in your release folder

14. Generate an md5sum.txt file for all of them:

    .. code::

        md5sum ./* > md5sum.txt
        
15. Verify that the filesize of .zsync blob is different from the one 
    stored on https://download.kde.org

    - for stable releases: https://download.kde.org/stable/krita/updates/Krita-Stable-x86_64.appimage.zsync
    - for unstable releases: https://download.kde.org/unstable/krita/updates/Krita-Beta-x86_64.appimage.zsync
    
    The filesize must be different, otherwise KDE's mirroring system will not 
    propagate the change automatically. If you see that the filesize is the same,
    notify sysadmins to update the mirrors manually.

    Please take it into account that "unstable" releases should have "Beta" in the zsync file name,
    **not** "Unstable" as you could guess. This word comes from `$CHANNEL` variable in `build_image.sh` script.

16. Upload all files to download.kde.org (or ask sysadmins to do that using this manual ftp://upload.kde.org/README):

Note that the msix file is only for uploading to the Windows Store, it doesn't need to be uploaded to download.kde.org.

    - to https://download.kde.org/unstable/krita/5.1.0-beta1/
        * krita-5.1.0-beta1.tar.gz
        * krita-5.1.0-beta1.tar.gz.sig
        * krita-5.1.0-beta1.tar.xz
        * krita-5.1.0-beta1.tar.xz.sig
        * krita-5.1.0-beta1-x86_64.appimage
        * krita-5.1.0-beta1-x86_64.appimage.sig
        * krita-x64-5.1.0-beta1-dbg.zip
        * krita-x64-5.1.0-beta1-setup.exe
        * krita-x64-5.1.0-beta1.zip
        * krita-x86-5.1.0-beta1-dbg.zip
        * krita-x86-5.1.0-beta1-setup.exe
        * krita-x86-5.1.0-beta1.zip
        * krita-5.1.0-beta1.dmg
        * krita-arm64-5.1.0-beta1.apk
        * krita-arm32-5.1.0-beta1.apk
        * krita-x86-5.1.0-beta1.apk
        * krita-x86_64-5.1.0-beta1.apk
        * md5sum.txt
    - to https://download.kde.org/unstable/krita/updates/
        * Krita-Beta-x86_64.appimage.zsync
        
    Please don't forget to replace "unstable" to "stable" for stable release builds. 
    It should be replaced for both, packages themselves and zsync file


17. Template ticket for sysadmins:

    .. code::

        Hi, sysadmins!

        Could you please do the final steps for publishing Krita release?

        There are two tasks:

        1) Upload release artifacts (20 files) to download.kde.org:

            * Source link: https://files.kde.org/krita/release-5.1.0-beta1/
            * Destination link: https://download.kde.org/unstable/krita/5.1.0-beta1/
            
        2) Upload updates ZSync artifacts (1 file) to download.kde.org:
            * Source link: https://files.kde.org/krita/release-5.1.0-beta1-updates/
            * Destination link: https://download.kde.org/unstable/krita/updates/
                         
        3) Add `Krita 5.1.0 Beta1` bugzilla version

18. Now the folder on download.kde.org should have 21(!) files. Check if you missed something (and you surely did! :) ).

19. Verify consistency of all ZSync AppImage update links using the special script:

    .. code:: shell

        cd krita/
        python build-tools/ci-scripts/show-updates-status.py

    It should show information like this:

    .. code::

        == Channel: Stable FAILED ==
        ZSync URL: https://download.kde.org/stable/krita/updates/Krita-Stable-x86_64.appimage.zsync
        ZSync exists: True
        AppImage exists: False
            MTime:  Wed, 06 Dec 2023 13:28:16 +0000
            Filename:  krita-5.2.2-x86_64.appimage
            URL:  https://binary-factory.kde.org/job/Krita_Release_Appimage_Build/124//artifact/krita-5.2.2-x86_64.appimage
            SHA-1:  16a1a640084446b45ea078d8b81cffc075144a02

        == Channel: Beta (unstable) FAILED ==
        ZSync URL: https://download.kde.org/unstable/krita/updates/Krita-Beta-x86_64.appimage.zsync
        ZSync exists: True
        AppImage exists: False
            MTime:  Thu, 14 Sep 2023 09:26:05 +0000
            Filename:  krita-5.2.0-rc1-x86_64.appimage
            URL:  https://binary-factory.kde.org/job/Krita_Release_Appimage_Build/121//artifact/krita-5.2.0-rc1-x86_64.appimage
            SHA-1:  4bd0f522c22f41e504bf1e9ced540fa11ed5ec53

        == Channel: Plus FAILED ==
        ZSync URL: https://cdn.kde.org/ci-builds/graphics/krita/krita/5.2/linux/Krita-Plus-x86_64.appimage.zsync
        ZSync exists: False
        AppImage exists: False

        == Channel: Next ==
        ZSync URL: https://cdn.kde.org/ci-builds/graphics/krita/master/linux/Krita-Next-x86_64.appimage.zsync
        ZSync exists: True
        AppImage exists: True
            MTime:  Tue, 02 Apr 2024 22:30:57 +0000
            Filename:  krita-5.3.0-prealpha-64b33ed808-x86_64.appimage
            URL:  https://cdn.kde.org/ci-builds/graphics/krita/master/linux/krita-5.3.0-prealpha-64b33ed808-x86_64.appimage
            SHA-1:  e360127c3c956499ed0266ad8eb9bcdad3789956

    Check the following:

        * none of the channels are marked with **FAILED**
        * AppImage's filename is set to the one you just uploaded
        * Appimage's URL is a full URL pointing to a seemingly correct location (see the definition of the "channels" above)
        * ``AppImage exists: True`` will tell you if the AppImage URL in downloadable, 
          so you don't have to recheck it yourself

    If you want to test ZSync manually, don't use the system-provided package. Use 
    this cli-tool provided by AppImage team: https://appimage.github.io/zsync2/

20. If you are doing **the first stable release** after branching-out, e.g. the first release of "Krita 5.3.0", then make sure 
    ask sysadmins to relink "Krita Plus krita/5.2" zsync file to "Krita Plus krita/5.3"

21. If you are doing **any stable release**, manually switch zsync file of Krita Beta to the Krita Stable, to make sure
    users will get updates.

22. If you are doing **any release from a stable branch**, manually update the version to the next one with suffix "alpha" to 
    make sure that Krita Plus packages correctly show it to the user.

23. Manually verify that the previous version of Krita AppImage can update to 
    the new one from the GUI. It should use the .zsync file uploaded above.
    
Release coordination
~~~~~~~~~~~~~~~~~~~~

1. Mail KDE release coordination <release-team@kde.org>
2. Send release notes for future Krita versions to news@publisher.ch
3. Create bugzilla version: https://bugs.kde.org/editversions.cgi?product=krita Or file a sysadmin ticket for that. 
4. [only for a major release] Warn kde sysadmins that we're going to release and that krita.org is going to take load. Just file a ticket on phabricator.

PR and Communications
---------------------

Pre-release
~~~~~~~~~~~

1. Update Kiki page
2. Update press pack and page
3. Verify if manual pages are updated, if not annoy @woltherav and add undocumented features to Krita: Manual
4. Notify people that they can start making release demonstrations.

Release
~~~~~~~

1. Update download page
2. Publish the announcement and release notes
3. Add release links to Release History section of the site: https://krita.org/en/about/krita-releases-overview/ 
4. Add the release to the org.krita.org.appdata.xml file in MASTER.

Post-release
~~~~~~~~~~~~

* tumblr (wolthera)
* BlenderArtists (wolthera)
* deviantart (wolthera)
* VK (dmitry)
* blendernation (halla)
* twitter (halla)
* facebook (halla)
* 3dpro (halla)
* reddit (raghukamath)

Notes
=====

Additional info can be found here:
https://phabricator.kde.org/T10762
