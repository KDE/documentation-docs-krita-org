.. .. meta::
   :description:
        Frequently asked Krita Questions.

.. metadata-placeholder

   :authors: - Scott Petrovic
             - Wolthera van Hövell tot Westerflier <griffinvalley@gmail.com>
             - Raghavendra Kamath <raghu@raghukamath.com>
             - Boudewijn Rempt <boud@valdyas.org>
             - Alvin Wong
             - Dmitry Kazakov
             - Timothée Giet
             - Tokiedian
             - Nmaghfurusman
             - RJ Quiralta
             - Tyson Tan
   :license: GNU free documentation license 1.3 or later.

.. index:: FAQ, Frequently Asked Questions
.. _faq:
.. _KritaFAQ:


#########
Krita FAQ
#########

This page contains common problems people have with Krita. Note that we assume that you are using the latest version of Krita. Please verify that to make sure.

.. contents::

General
=======

General questions

What is Krita?
--------------

This is our vision for the development of Krita:

    Krita is a free and open source cross-platform application that offers an end-to-end solution for creating digital art files from scratch. Krita is optimized for frequent, prolonged and focused use.
    Explicitly supported fields of painting are illustrations, concept art, matte painting, textures, comics and animations.
    Developed together with users, Krita is an application that supports their actual needs and workflow. Krita supports open standards and interoperates with other applications.

Is it possible to use Krita in my own language, not English?
------------------------------------------------------------

Krita should automatically use the system language. If that is not the case, please follow these steps:

#. With :menuselection:`Settings --> Switch Application Language...` menu item will appear a small window.
#. Click :guilabel:`Primary language` and select your language.
#. Click :guilabel:`OK` to close the window.
#. Restart krita and it will be displayed in your selected language!

If this doesn't work, you might have to add a fall-back language as well. This is a bug, but we haven't found the solution yet.

I have a problem, how to get support for Krita?
-----------------------------------------------

#. Ask your question on one of the user support forums. It can be `Krita Artists forum <https://krita-artists.org/>`_ (recommended), `Krita KDE forum <https://forum.kde.org/viewforum.php?f=136>`_ or alternatively `Krita subreddit <https://forum.kde.org/viewforum.php?f=136>`_ .

#. Remember -- most probably the person you're interacting with is a volunteer, and even if not, it's not someone actually paid for doing user support. Treat them nicely and respect their time! They will for sure reciprocate that.

#. Create a new thread or post for your issue and state the issue in the title. Even if you don't know how to describe it exactly, for example you title the post "Krita's text tool is acting weird", it is much better than simple "Help!".

#. Describe your issue. You can add screenshots and videos, but even if you do that, write a few words what the video shows and what the issue is.

#. State all relevant details: most importantly your operating system (Windows, MacOS, Linux...), which version of Krita you use (go to :menuselection:`Help -> About Krita` to find out) and what kind of tablet you have (if your issue is related to a tablet driver).

#. Answer all questions your supporter asks, even if you don't think they're relevant. They probably have a reason to ask about that.

#. If you don't know the answer or you don't know how to get the information your supporter asks for, don't hesitate to ask for clarification.

#. If you mentioned an issue, please help with testing if you're asked to do that -- that will speed up the process of finding the cause and preparing a fix.



Does Krita have layer clip or clipping mask?
--------------------------------------------

Krita has no clipping mask, but it has a clipping feature called
inherit alpha. Let's see :ref:`this page <clipping_masks_and_alpha_inheritance>` and learn how to do
clipping in Krita!

Where are the configuration files stored?
-----------------------------------------

These are stored at the following places for the following operating
systems:

Linux
    :file:`$HOME/.config/kritarc`
Windows
    :file:`%APPDATA%\\Local\\kritarc`
MacOS X
    :file:`$HOME/Library/Preferences/kritarc`

The kritarc file is the configuration file. Krita does not store settings in the Windows registry.

.. _faq_reset_krita_configuration:

Resetting Krita configuration
-----------------------------

You can reset the Krita configuration in one of the following ways:

-  Press and hold :kbd:`Shift + Alt + Ctrl` while starting Krita. This should show a pop-up asking if you want to reset the configuration. Press :guilabel:`yes` to reset it.

-  For Krita 3.0 and later: Delete/rename the kritarc file, found here:

    Linux
        :file:`$HOME/.config/kritarc`
    Windows
        :file:`%LOCALAPPDATA%\\kritarc`
    MacOS X
        :file:`$HOME/Library/Preferences/kritarc`

There can be two other files you might want to remove: kritaopenglrc and
kritadisplayrc.

If the configuration was causing a crash, don't delete the mentioned file, but instead rename and
send it to us in order for us to figure what caused the crash.

If you have installed Krita through the Windows store, the kritarc file will be in another location

:file:`%LOCALAPPDATA%\\Packages\\49800Krita_{RANDOM STRING}\\LocalCache\\Local\\kritarc`

The random string depends on your installation.

Windows users have a habit of uninstalling and reinstalling applications to solve problems. Unless the problem is that the installation was corrupted by a virus scanner or drive failure, that will NOT work. Uninstalling Krita then reinstalling replaces the bytes on your drive with exactly the same bytes that were there before. It doesn't reset anything, least of all Krita's settings.



Why my configuration resets on its own?
---------------------------------------

There are two possible reasons:

- You don't save your settings. 

This is most probable if you are on Windows and you have either a display with a small resolution (below fullHD) or if you have fullHD resolution with UI scaling in Windows settings (which is 150% by default). In those cases it might happen that you don't see the :guilabel:`OK` button in the :guilabel:`Configure Krita` dialog. You can use :kbd:`Alt + O` instead. (You can go to :menuselection:`Configure Krita... --> General --> Window` and make sure that :guilabel:`Enable HiDPI` checkbox is unchecked to disable scaling for Krita and get a smaller UI).

- You close your computer using the power button.

If you are on Windows and you use power button instead of a standard procedure to close or restart your computer, it might happen that Krita's configuration file gets corrupted. To solve this, just use the correct way of closing your system: either :menuselection:`Start -> Restart` or :menuselection:`Start -> Shutdown`.

Where are my resources stored?
------------------------------

Linux
    :file:`$HOME/.local/share/krita/`
Windows
    :file:`%APPDATA%\\krita\\`
Mac OS X
    :file:`~/Library/Application Support/Krita/`

If you installed Krita in the Windows Store, your custom resources will be in a location like:
    :file:`%LOCALAPPDATA%\\Packages\\49800Krita_{RANDOM STRING}\\LocalCache\Roaming\krita`
    
Krita tells me it can't find some files and then closes, what should I do?
--------------------------------------------------------------------------

Causes for this could be the following:

-  It might be that your download got corrupted and is missing files (common with bad wifi and bad internet connection in general), in that case, try to find a better internet connection before trying to download again. Krita should be around 80 to 100 MB in size when downloading.
-  It might be that something went wrong during installation. Check whether your harddrive is full and reinstall Krita with at least 120 MB of empty space. If not, and the problem still occurs, there might be something odd going on with your device and it's recommended to find a computer expert to diagnose what is the problem.
-  Some unzippers don't unpack our ZIP files correctly. The native ones on Windows, OSX and most Linux distributions should be just fine, and we recommend using them.
-  You manually, using a file manager deleted or moved resources around, and thus Krita cannot find them anymore.

What Graphics Cards does Krita support?
---------------------------------------

Krita can use OpenGL to accelerate painting and canvas zooming, rotation and panning. Nvidia and recent Intel GPUs give the best results. Make sure your OpenGL drivers support OpenGL 3.2 as the minimum. AMD/ATI GPU’s are known to be troublesome, especially with the proprietary drivers on Linux. However, it works perfectly with the Radeon free driver on Linux for supported AMD GPU. Try to get a graphics card that can support OpenGL 3.2 or above for the best results, some examples:

.. Following graphics cards have been suggested by Tyson Tan on the basis that they all support 3.2

Intel
    Intel 3rd Generation HD Graphics, IvyBridge or Bay-Trail microarchitecture, released in 2012. Commonly available products: Celeron J1x00, N2x00, Celeron (G)1xx0, Pentium J2x00, N3500, Pentium (G)2xx0, Core i3/5/7-3xx0.
AMD/ATI
    Radeon HD 2000 family, TeraScale 1 microarchitecture, Released in 2007. Commonly available products: Radeon HD 2400 PRO, Radeon HD 2600 PRO, etc.
Nvidia
    GeForce 8 family, Tesla microarchitecture, released in 2006. Commonly available products: GeForce 8400 GS, GeForce 8800 GTS, 9800 GTX, GTS 250, etc.

*For Krita 3.3 or later:* Krita on Windows can use Direct3D 11 for graphics acceleration (through ANGLE). This is enabled automatically on systems with an Intel GPU.

I can't edit text from PSD files created by Photoshop
-----------------------------------------------------

There is no text support for PSD file yet. The text will appear rasterized and converted into a paint layer.

How much memory does my image take?
-----------------------------------

For simple images, its easy to calculate: you multiply width \* height \* channels \* size of the channels (so, for a 1000×1000 16 bit integer rgba image: 1000 x 1000 x 4 x 2). You multiply this by the number of layers plus two (one for the image, one for the display). If you add masks, filter layers or clone layers, it gets more complicated.

Why do I get a checkerboard pattern when I use the eraser?
----------------------------------------------------------

You’re probably used to Gimp or Photoshop. The default background or first layer in these applications doesn’t have an alpha channel by default. Thus, on their background layer, the eraser paints in the background color.

In Krita, all layers have an alpha channel, if you want to paint in the background color, you should simply do it in a layer above the first one (Layer 1), that would prevent  you from erasing the white background color, making the checkerboard visible. You get the same effect in, say, Gimp, if you create new image, add an alpha channel and then use the eraser tool. Most Krita users will actually start a sketch in Krita by adding a new blank layer first before doing anything else. (The :kbd:`Ins` key is a useful shortcut here). That doesn’t use extra memory, since a blank layer or a layer with a default color just takes one pixel worth of memory.

Can krita work with 8 bit (indexed) images?
-------------------------------------------

No. Krita has been designed from the ground up to use real colors, not indexed palettes. There are no plans to support indexed color images, although Krita can export to some indexed color image formats, such as GIF. However, it does not offer detailed control over pixel values.


Where can I find older versions of Krita?
-----------------------------------------

All the older versions of Krita that are still available can be found here:

-  `Very old builds <https://download.kde.org/Attic/krita/>`_.

On Windows, the Krita User Interface is too big on my screen
------------------------------------------------------------

If you're using Windows, you can set the display scaling to 150% or 200%. Krita comes with HiDPI enabled by default, so if you do that, the Krita UI might be too big for your screen. You can turn it off using the following steps:

- On the menu, select :menuselection:`Settings --> Configure Krita...`
- On :guilabel:`General` page, switch to :guilabel:`Window` tab.
- Uncheck :guilabel:`Enable Hi-DPI support` (or check if you wish to enable it)
- Press :guilabel:`OK`, if the settings screen is too big, :kbd:`Alt + O` will trigger the OK button too.
- Restart Krita

You can also change the toolbox icon size by right-clicking on the toolbox and selecting a size.

Windows: In fullscreen mode, why is there a thin gap at the bottom of the window?
---------------------------------------------------------------------------------

When :ref:`Canvas Graphics Acceleration <display_settings>` is set to OpenGL, you may see a thin gap at the bottom of the window which you can see through. This is done deliberately to work around a bug causing menus and dropdowns to be unusable. If you find it distracting, you can consider changing the Renderer to Direct3D 11 which doesn't require this workaround.

Windows: OBS can't record the Krita OpenGL canvas
-------------------------------------------------

The possible workarounds for this is to do either of the following:

#. Turn off OpenGL in :menuselection:`Settings --> Configure Krita... --> Display`.
#. Or don't use the hardware accelerated mode (game recording mode) in
   OBS, thus capturing the whole desktop instead of attempting to capture
   only Krita.

You might also be able to work around the problem by using the ANGLE renderer instead of native OpenGL.

Windows: Can I use Krita with Sandboxie?
----------------------------------------

No, this is not recommended. Sandboxie causes stuttering and freezes due to the way it intercepts calls for resources on disk.

Windows: Krita cannot save
--------------------------

If the message is "File not found. Check the file name and try again.", you probably have Controlled Folder Access enabled.

-   Select :menuselection:`Start --> Settings`.
-   Choose :menuselection:`Update & security --> Windows Defender`.
-   Select :guilabel:`Open Windows Defender Security Center`.
-   Select :guilabel:`Virus & threat protection`, and then choose :guilabel:`Virus & threat protection settings`.
-   Under :guilabel:`Controlled folder access`, turn it on or off.

You can also whitelist Krita, following `these instructions <https://docs.microsoft.com/en-us/windows/security/threat-protection/microsoft-defender-atp/customize-controlled-folders#allow-specific-apps-to-make-changes-to-controlled-folders>`_.

Windows: Krita cannot open my file anymore
------------------------------------------

Your file got corrupted. There are several things that might cause this:

#. Windows was shutdown improperly, like by holding the power button. This prevents your harddrive from finishing up the things it is doing and file away your files incorrectly. Please always try to shutdown your computer via the proper shutdown procedure, and if you are in a situation where this is not possible (like frequent blackouts), make daily backups! This may lead to the file being filled with zeroes, so it cannot be recovered from.

    .. versionchanged:: 4.2.8
        
        Krita version 4.2.8 introduced special safety measure for Windows that should help avoiding this situation. But in any case, unless something makes it impossible, always make sure to shutdown your system using the standard approach. On Windows that means going to Start menu and selecting "Shutdown".

#. Badly programmed security software may attempt to rewrite KRA files, or prevent Krita from writing to the folder you wish to save to. These cases can be checked by trying to save in that location, and then, without shutting down Krita, checking in the folder to see if the file saved. Files lost due this cannot be recovered.
#. Cloud services like dropbox and onedrive have been known to prevent Krita from saving. We've implemented fixes for this, but much like the above point it is worth checking that this isn't the cause of the issue. Files lost due this cannot be recovered.
#. Occasionally the ZIPs that KRA files comprise of will have the last few bytes missing. We're doing everything in our power to prevent this kind of corruption, but it might be a file system issue. This particular bug can be fixed by renaming the extension (in windows you will need to enable the file extensions, which this FAQ will not cover) to ZIP, and then using a ZIP repairing utility to fix the ZIP file. Then rename it back to KRA.
#. If Krita doesn't give an error message, but rather crashes, your file is too big, and Krita is not so much crashing as that the operating system is shutting it down. Try shutting down some other programs like webbrowsers or streaming services to free up working memory. You should be able to open the file in question. At this point the recommended course of action is to try and reduce the file size in some manner, such as merging layers, splitting up an animation or scaling the image down.


How to recover my files?
-------------------------
#. Check whether you have any backup file or autosave left: :ref:`autosave`.
#. Check whether you can open the file as ZIP archive.
    #. Rename the extension of the file from ``.kra`` to ``.zip``.
    #. Try to open (your system should automatically select an archive opener tool).
    #. There is file called mergedimage.png inside that represents all layers merged that you can use for reference in case you can't restore anything else.
#. Check whether ZIP repairer tool helps.
    #. Copy the file so you have a backup just in case.
    #. Rename the extension of the file from ``.kra`` to ``.zip``.
    #. Use ZIP repairer tool on the ``.zip`` file.

        .. code-block:: bash
        
            # On Linux:
            mv file.kra file_copy.zip
            zip -F file_copy.zip --out file_new1.zip
            unzip file_new1.zip
            # if it still doesn't work:
            zip -FF file_copy.zip --out file_new2.zip
            unzip file_new2.zip
            # if it still doesn't work, try to run it again on *file_new2.zip* file, or try on *file_new1.zip* file

            # On Windows:
            Copy the file, rename the extension.
            Use any graphical ZIP repairer on the new file. (Follow the instructions for that specific program).


    #. Try to open in Krita.
    #. If it cannot be opened in Krita, try the trick from 2.: open the archive and find mergedimage.png file.

#. Open your file in Notepad or any other text editor. If the the content of the file is only a repeated *NUL* symbol, it means the file is most probably unrecoverable using the standard method. If it's of a very high importance for you, you can try to recover the previous save using methods that checks the hard drive directly.


Krita crashes on Windows 7 on start-up
--------------------------------------

Starting with Krita 4.2.0, Krita uses version 5.12 of the Qt toolkit. This needs to have access to Direct3D 11 or OpenGL ES 2.0 or higher. You might need to install drivers appropriate to your GPU (Nvidia, AMD/ATI, Intel). This also makes it hard to run Krita in a virtual environment: in Virtual Box you need to install the guest addition in safe mode, and enable the experimental Direct3D support. 


Windows: How can I produce a backtrace?
-----------------------------------------

.. seealso::

    :ref:`Dr. Mingw debugger <dr_minw>`

If you experience a crash on Windows, and can reproduce the crash, the bug report will be much more valuable if you can create a backtrace. A backtrace is somewhat akin to an airplane's blackbox, in that they tell what set of instructions your computer was running when it was crashing (where the crash happened), making it very useful to figure out why the crash happened.

The :ref:`Dr. Mingw debugger <dr_minw>` is bundled with Krita. Please visit the page :ref:`Dr. Mingw debugger <dr_minw>` for instructions on getting a backtrace with it.

Windows: Krita's window is semi-transparent
-------------------------------------------

Chances are you are using an NVidia GPU. Due to a bug in Nvidia's driver that we haven't been able to workaround yet, sometimes Krita's window will be transparent or semi-transparent. The solution is to enable the Angle renderer in Krita's Settings dialog. Open the :menuselection:`Settings` menu (Press Alt-N if the menubar is not visible and your system is in English), then open the :guilabel:`Configure Krita` dialog. In the dialog window select the :guilabel:`Display` page and select the Angle renderer in the :guilabel:`Preferred Renderer` combobox. Restart Krita.


Tablets
=======

What tablets does Krita support?
--------------------------------

Krita isn’t much fun without a pressure sensitive tablet. If the tablet has been properly configured, Krita should work out of the box. 

On Windows, you need to either install the Wintab drivers for your tablet, or enable the :guilabel:`Windows 8+ Pointer Input` option in Krita's settings.

You can find a community curated list of tablets supported by krita :ref:`here <list_supported_tablets>`.

If you're looking for information about tablets like the iPad or Android tablets, look :ref:`here <krita_android>`.


What if your tablet is not recognized by Krita?
-----------------------------------------------

First, check if you have installed drivers and the like. The :ref:`drawing_tablets` page has some explanations and descriptions of common issues. If none of those work, we would like to have a bug report at bugs.kde.org, with a tablet log. Here's how you make a tablet log:

#. You need to have something to output the log to. On 4.2 you can use the :ref:`log_viewer` docker for this. Just open the log viewer, and enable logging.
    
    .. versionchanged:: 4.2
    
        The log viewer got added to Krita in 4.2, so for older versions of Krita, you will need to either run Krita in the terminal if you have Linux or MacOS, or for Windows install `DebugView <https://docs.microsoft.com/en-us/sysinternals/downloads/debugview>`_ from the official Microsoft site, start DebugView and then start Krita.
        
        When using a terminal, make sure to enable 'unlimited scrollback'.

#. Press the :kbd:`Ctrl + Shift + T` shortcut, you will see a message box telling the logging has started.
#. Try to reproduce your problem, you will be able to see the log being created in the log viewer as you draw.
#. Save the output from the log viewer into a txt file, and attach it to the bugreport.

On Linux, it is also useful to have the following information:

#. ``lsmod``
#. ``xinput``
#. ``xinput list-props`` (id can be fetched from the item 2)

However, in 100\% of the cases where Windows users have reported that their tablet didn't work over the past five years, the problem has been either a buggy driver or a broken driver installation, but not a bug in Krita.
   
   
How to fix a tablet offset on multiple screen setup on Windows
--------------------------------------------------------------

If you see that your tablet pointer has an offset when working with Krita canvas, it might be highly likely that Krita got an incorrect screen resolution from the system. That problem happens mostly when an external monitor is present and when either a monitor or a tablet was connected after the system booted.

You can configure this by going to the :ref:`tablet_settings`.

Microsoft Surface Pro and N-Trig
--------------------------------

Krita 3.3.0 and later supports the Windows Pointer API (Windows Ink) natively. Your Surface Pro or other N-Trig enabled pen tablet should work out of the box with Krita after you enable Windows Ink in :menuselection:`Settings --> Configure Krita... --> Tablet`.

Tablet Pro and the Surface Pro
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Unlike Wacom's Companion, the Surface line of tablets doesn't have working hardware buttons. Tablet Pro is a (non-free) utility that puts virtual buttons on screen. Krita 3.1 and above will have predefined shortcut profiles to work with Tablet Pro.

https://tabletpro.com/

See https://www.youtube.com/watch?v=WKXZgYqC3tI for instructions.

Weird stuff happens on Windows, like ripples, rings, squiggles or poltergeists
------------------------------------------------------------------------------

Windows comes with a lot of settings to make it work with a pen. All these settings can be annoying. This tool can help you set the settings correctly when you're using a tablet:

https://github.com/saveenr/Fix_My_Pen/releases

Touch doesn't seem to work on Windows
-------------------------------------

You might have to disable and enable the touch driver: go to the device manager. (Click the :guilabel:`Start` button and type device manager). Choose HID (User interface devices or something like that). Choose Intel(R) Precise Touch Device. Right click, Disable it. Right click, Enable it.

Toolbox
=======

Toolbox missing
---------------

You can reset the Workspace by pressing the right most button on the toolbar, the Workspace switcher, and click on a desired Workspace from the list.

Or you can right-click on any docker title bar or open space in any toolbar, and select Toolbox. It's the first option.

Also, you can check the :guilabel:`Settings` menu, it has got a lot of interesting stuff, then go to the Dockers menu and select :guilabel:`Toolbox`.

Tool icons size is too big
--------------------------

Right click the toolbox to set the size.

Krita can't get maximized
-------------------------

This happens when your dockers are placed in such a way that the window cannot be made less high. Rearrange your Workspace.

Resources
=========

Is there a way to restore a default brush that I have mistakenly overwritten with new settings to default?
----------------------------------------------------------------------------------------------------------

Yes. First go to the resource folder, which is in

Linux
    :file:`$HOME/.local/share/krita/`
Windows
    :file:`user\\Appdata\\Roaming\\krita\\` or :file:`%APPDATA%\\Roaming\\krita\\`
OSX
    :file:`~/Library/Application Support/Krita/`

You can easily do this by going into :menuselection:`Settings --> Manage Resources... --> Open Resource Folder`.

Then go into the *paintoppresets* folder and remove the latest created
file that you made of your preset.

After that go back to the resources folder and edit the blacklist file to
remove the previous paintoppreset so Krita will load it. (Yes, it is a
bit of a convoluted system, but at the least you don't lose your
brushes)

How do I set favorite presets?
------------------------------

Right-click a brush in the brush docker and assign it a tag. Then right-click on canvas to call popup palette, click the second right-most icon on the bottom-right of the palette, now you can pick the tag which contains the brush you assigned to it.

Can Krita load Photoshop Brushes?
---------------------------------

Yes, but there are limitations. You can load ABR files by using the :guilabel:`Import` button in the :guilabel:`Predefined brush` tab in the brush editor. Since Adobe hasn’t disclosed the file format specification, we depend on reverse-engineering to figure out what to load, and currently that’s limited to basic features.

Krita is slow
=============

There is a myriad of reasons why this might be. Below is a short checklist.

-  Something else is hogging the CPU or the memory: spotify and other electron apps have been known to do this.
-  You are running Windows, and have 3rdparty security software like Sandboxie or Total Defender installed
-  You are working on images that are too big for your hardware (dimensions, channel depth or number of layers)
-  You do not have canvas acceleration enabled
-  You have (NVidia) Vertical Sync enabled

Please also check `this page <https://phabricator.kde.org/T7199>`_.

Slow start-up
-------------

You probably have too many resources installed. Deactivate some bundles under the :menuselection:`Settings --> Manage Resources...` menu item.

If you're using Windows with the portable ZIP file, Windows will scan all files every time you start Krita. That takes ages. Either use the installer or tell Microsoft Security Essentials to make an exception for Krita.

Slow Brushes
------------

-  Check if you accidentally turned on the stabilizer in the tool options docker.
-  Try another scaling mode like trilinear. :menuselection:`Settings --> Configure Krita... --> Display`.
-  Try a lower channel depth than 16-bit.
-  For NVidia, try a 16-bit floating point color space.
-  For older AMD CPU's (Krita 2.9.10 and above), turn off the vector optimizations that are broken on AMD CPUs. :menuselection:`Settings --> Configure Krita... --> Performance`. This isn't needed if you've got an AMD Threadripper™ CPU.
-  It's a fairly memory hungry program, so 2GB of RAM is the minimum, and 4GB is the preferable minimum.
-  Check that nothing else is hogging your CPU.
-  Check that Instant Preview is enabled if you're using bigger brushes (but for very small brushes, make sure is disabled).
-  Set brush precision to 3 or auto.
-  Use a larger value for brush spacing.
-  If all of this fails, record a video and post a link and description on the Krita forum.
-  Check whether OpenGL is enabled, and if it isn't, enable it. If it is enabled, and you are on Windows, try the Angle renderer. Or disable it.

Slowdown after a been working for a while
-----------------------------------------

Once you have the slowdown, click on the image-dimensions in the status bar. It will tell you how much RAM Krita is using, if it has hit the limit, or whether it has started swapping. Swapping can slow down a program a lot, so either work on smaller images or turn up the maximum amount of RAM in :menuselection:`Settings --> Configure Krita... --> Performance --> Advanced Tab`.

Animation
=========

Why is my animation black in my video player
--------------------------------------------

You did not render the animation using the "baseline" option and you are using the default Windows media player. Re-render using the baseline option or use a better video player application, like VLC. Check `this useful diagram <https://www.deviantart.com/tiarevlyn/art/T-Krita-4-1-7-rendering-issues-manual-783473428>`_.


Tools
=====

Why does the Transform Tool give a good result and then get blurry upon finalizing?
-----------------------------------------------------------------------------------

The transform tool makes a preview that you edit before computing the finalized version. As this preview is using the screen resolution rather than the image resolution, it may feel that the result is blurry compared to the preview. See `this page <https://forum.kde.org/viewtopic.php?f=139&t=127269>`__ for more info.


License, rights and the Krita Foundation
========================================

Who owns Krita?
---------------

The Stichting Krita Foundation owns the Krita trademark. The copyright on the source code is owned by everyone who has worked on the source code.

Who and what is Kiki?
---------------------

Kiki is a cybersquirrel. She’s our mascot and has been designed by Tyson Tan. We choose a squirrel when we discovered that ‘krita’ is the Albanian word for Squirrel.

Why is Krita Free?
------------------

Krita is developed as `free software <https://www.gnu.org/>`_ within the KDE community. We believe that good tools should be available for all artists. You can also buy Krita on the Windows Store if you want to support Krita's development or want to have automatic updates to newer versions.

Why isn't Krita on Steam and in the Windows Store Free?
-------------------------------------------------------

Krita on Steam and in the Windows Store is still Free and Open Source software; the binaries are exactly the ones you can also download from krita.org. We've put a price tag on downloading Krita from either store to support Krita's development. Nobody is getting rich out of it, but the income from Steam and the Windows Store currently pays for the full-time involvement with Krita of four developers. See `Krita Available from the Windows Store <https://krita.org/en/item/krita-available-from-the-windows-store/>`_ for more information.


Can I use Krita commercially?
-----------------------------

Yes. What you create with Krita is your sole property. You own your work and can license your art however you want. Krita’s GPL license applies to Krita’s source code. Krita can be used commercially by artists for any purpose, by studios to make concept art, textures, or vfx, by game artists to work on commercial games, by scientists for research, and by students in educational institutions.

If you modify Krita itself, and distribute the result, you have to share your modifications with us. Krita’s GNU GPL license guarantees you this freedom. Nobody is ever permitted to take it away.

.. _krita_android:
.. _krita_ios:

Can I get Krita for iPad? for Android?
--------------------------------------

Not for iOS or iPadOS at this point in time. Android is being worked on, but it will not have a phone or tablet, but the same desktop ui as always.

Who translates Krita
--------------------

Krita is a `KDE application <https://www.kde.org/>`_ — and proud of it! That means that Krita’s translations are done by `KDE localization teams <https://l10n.kde.org/>`_. If you want to help out, join the team for your language! There is another way you can help out making Krita look good in any language, and that is join the development team and fix issues within the code that make Krita harder to translate.

Reference
=========

https://answers.launchpad.net/krita-ru/+faqs
