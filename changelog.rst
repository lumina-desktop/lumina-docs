.. _Changelog:

Changelog
*********

This section describes the major features and changes to each version of Lumina, with the most recent version of Lumina listed first.

.. index:: changelog
.. _Lumina 0.9.0:

Lumina 0.9.0
============

* Changed the default wallpapers for Lumina/PC-BSD and added some more 4K Lumina wallpapers.

* Updated lumina-screenshot: Added a new quicksave option and launch editor button for opening a full editor, windows to be snapshot may now be clicked on 
  for selection rather than using the list of open windows, and screenshots may be cropped as needed within the utility before saving them to a file.
 
* Added new Utility: lumina-textedit. This is a simple plaintext editor with syntax highlighting, find/replace support, line numbers, and bracket highlighting.

* Updated the Lumina theme engine to no longer use stylesheets to modify non-desktop applications (including the Lumina tools/utilities). 
  This opens the door for a full Qt5 theme plugin to be used for non-desktop utilities instead.

* Updated which XDG mime-types are used for the default web browser and file manager. 
  This should make it align a bit better with what applications expect (if they try to read/use the database directly - such as some popular web browsers do).

* Updated Linux harddrive device detection ("nvme" devices).

* Added Gentoo Linux support and an "ebuild" file.

* Cleanup of some minor source syntax issues with Qt 5.6

* Fixed a number of multi-monitor issues. Screen resizes/changes will now be properly detected on the fly (on any system - including VM's), and panels will be placed properly on monitors not aligned with the y=0 axis.

* Ensured the current system volume gets saved on logout so it can be reloaded on next login (in case the volume was changed by some external tool during the session).

* Added new startup binary: "start-lumina-desktop". This will be used as the primary "entry point" for launching the desktop as opposed to the "Lumina-DE" binary (please adjust your .xinitrc files and wrapper scripts as needed). 
  The xsession desktop entry that Lumina installs was already changed to run this tool, so graphical desktop managers should be unaffected by this change. 
  This tool will eventually be used to perform the X session setup/configuration (so CLI users will not need to run xinit or startx directly anymore), but the X integration has not been implemented yet.

* Updated the FreeBSD appstore shortcut to point to the new appcafe.desktop file from PC-BSD.

* Cleaned many old shell scripts from the source tree (not needed for builds any more).

* Streamlined the build procedures slightly.

* Reorganized the source tree. Now all the Lumina tools/utilities are kept separate from the general build scripts/files within a src-qt5 directory, and additionally organized into categories (core, core-utils, desktop-utils).
  Automated build systems should not be impacted by this change, as the main project file (lumina.pro) has been left in the same place within the repository and just had all the internal paths adjusted accordingly.
 
* Updated all the installed desktop entries to use relative paths for the icons (better cross-OS support).

* Fixed the detection of "sloppy" URL's given to lumina-open.

* Adjusted one of the include files for the Lumina library so external applications can now link against the lib without the availability of the Lumina source tree (although still not recommended).

* Stability fix for the desktop when an invalid desktop plugin is set/registered.

.. index:: changelog
.. _Lumina 0.8.8:

Lumina 0.8.8
============

* Add 3 different view modes for applications in the start menu: Alphabetical (no categories), Partial Categories, or Categories (need to click the category to go into it and see the
  applications).
    
* Make the symlink icon overlays a bit smaller at 1/3 icon size instead of 1/2.

* Add a new button for the audio controls to the left side of the  :menuselection:`Start --> Preferences` menu for muting and unmuting audio.
    
* The RPM spec for Fedora/CentOS has been refactored.  Within the limits of supporting both Fedora and CentOS 7, 32-bit and 64-bit builds can be done from the same spec, so that it complies
  with Fedora's guidelines on how a package should be structured. 
    
* Improvements to the notepad desktop plugin.
    
* Redo the "App Menu" panel plugin so that it uses a self-contained menu and lists the logout options at the bottom.
    
* Fix sorting of "favorites" items in the "Start" menu to be sorted by display name instead of file name.
    
* Add new options for loading new wallpaper files in :command:`lumina-config`: Single Directory (all images within the directory) and Recursive Directory (all images in the selected
  directory and all sub-directories).
    
* Add support for selecting a ZFS snapshot by name, in addition to the current time-slider.

* NetBSD is now a supported build target.
    
* Add the ability to change monitor resolutions in :command:`lumina-xconfig`.
    
* Add support for the Intel backlight, if available, on FreeBSD systems.

* Fixed a translation bug for the Portuguese language.
   
* Fix a crash on FreeBSD 11.x when removing a desktop icon.
    
* Fix a multi-threading issue randomly causing :command:`lumina-fm` to crash when opening a directory.
    
* Fix some resize bugs with the custom resizeMenu class which is used by the "Start" menu.
   
* Multiple fixes for resolution detection as well as graphical glitches that were causing menus to behave unpredictably.

.. index:: changelog
.. _Lumina 0.8.7:

Lumina 0.8.7
============

* Convert everything to XCB and remove XLib dependencies.

* Update DragonFlyBSD support.

* Adjust build procedures to better support multiple concurrent threads using the "-j<#threads>" :command:`make` option.

* Add better relative path support for launching applications in the mimetype database.

* Add support for a new instance of a LuminaSingleInstance application using the "-new-instance" CLI flag.

* Add better fallback methodology for detecting and fixing stale single-instance flags.

* Now uses the Qt5-Concurrent build module for additional multi-threading support in various utilities.

* Add support for selecting a mouse cursor theme (requires session restart).

* Add new color schemes: Grey-Dark, Solarized-Light, Solarized-Dark, and Blue-Light.

* Customize the Lumina-default theme.

* Add inheritance to theme files and convert the Lumina-default to inherit the "None" theme.

* Add support to :ref:`Lumina Screenshot` for multi-screen arrangements and for including and excluding window borders for single window snapshots.

* Add support for various background image scaling and placement options.

* Add a number of new desktop shortcuts for the session. This requires existing users to remove their :file:`~/.lumina/fluxbox-keys` before logging in to get the new settings.

* Clean up the panel activation and detection routines to better respond to mouse-over events, particularly for auto-hidden panels.

* Completely overhaul the desktop plugin container system. Now it is completely drag and drop based with an intelligent grid of items and locations. Right-click, or click and hold, an item
  to open a menu of additional plugin configuration options. Note that any previous plugin locations will be reset to their defaults during the update to this new system.

* Add support for dropping files and directories from other applications onto the desktop, creating a symlink to the desktop folder when appropriate.

* Add font outlining to all desktop items so that the text is visible even if the font color blends into the background image.

* ZFS snapshot browsing is now seemlessly embedded within the directory viewer of :ref:`Insight File Manager`.

* Add support for either tabs or columns when viewing multiple directories at once.

* Replace the "Icon View" mode with the ability to adjust the icon sizes as desired.

* Add support for running the slideshow viewer and multimedia player in the background as separate tabs. Add the ability to zoom in/out on a slideshow image as desired.

* Add full drag and drop implementation to Insight File Manager. Can drag files and directories to external applications that support the standard "text/urilist" Mimetype for drag and drop
  operations.

* Directory and thumbnail loading is now a couple orders of magnitude faster than before. The thumbnail loading routine is now a completely separate background thread, preventing any delays
  in application functionality while loading.

* Add support for the "back" mouse button when viewing a directory.

* Completely overhaul the :ref:`Lumina File Information` utility. Now it is an almost complete front-end for the Qt/Lumina file information and XDG entry structures.

* Add support for detecting and allowing user-local Fluxbox themes in addition to system-local themes.

* Decrease initial loading time of :ref:`Lumina Configuration` by making it load all the background image thumbnails on demand instead of up-front.

* Update the :ref:`Interface` used for panel configuration so that it is much easier to read and use.

* Update the application selection in the fileopen dialog of :ref:`Lumina Open`, making it much easier to find the proper application to open the specified file.

* Overhaul the "Clock" panel plugin. Now it provides a menu with a calendar as well as an option for the user to instantly switch the time zone.

* New "Start Menu" panel plugin is a Windows-esque system menu which incorporates the functionality of both the user button and the system dashboard in one place. This plugin also supports
  creating and removing desktop links for applications, as well as "quick-launch" buttons for adding applications to the panel.
  
* Update the "Workspace Switcher" panel plugin so it stays in sync with external changes to the current workspace.

* New "Line" panel plugin provides a simple visual line to provide separation between plugins.

* Fix or bypass some Fluxbox window placement bugs.

* Fix some bugs in the user button regarding file and directory removals.

* Clean up a number of built-in text strings for clarity and consistency.

* Ensure that graphical sliders for adjusting screen brightness only go down to 10% to prevent the user from blacking out their screen entirely.

* Update the support for non-xterm terminal emulators to be opened within a particular directory.

* Update URL syntax handling in :ref:`Lumina Open`.

* Update support for sticky windows to appear in the task manager on all workspaces.

* Clean up a number of possible bugs with regards to how external application might be launched or used. This fixes the random race condition where a process finished but the thread in
  Lumina which called it still thinks it is running.

* Ensure that all calendar widgets on the desktop or panel update as necessary to ensure the correct date is shown during multiple-day sessions.

* Add a small CLI flag to :ref:`Lumina Open` for testing the crash handler ("-testcrash").

* Ensure that on FreeBSD, the disk I/O information uses instantaneous values instead of system averages.

.. index:: changelog
.. _Lumina 0.8.6:

Lumina 0.8.6
============

* Add the ability to set system-locale overrides, used on login. This allows the user to mix locale settings for the various outputs.
        
* Add the ability to switch the locale of the current session on the fly, changing all locale settings for the current session only. These settings will be used when launching any
  applications within that session.
        
* Fix up the translation mechanisms so that everything is instantly re-translated to the new locale.
        
* More languages are now fully translated. Install the x11/lumina-i18n port or pkg to install the localizations and enable these new localization features.
    
* Add support for the “Actions” extension to the XDG Desktop specifications. This allows applications to set a number of various actions, or alternate startup routines, within their XDG
  desktop registration file. These actions are shown within Lumina as new sub-menus within the "Applications" menu as well as in the "User" button. Look for the down arrow next to the
  application's icon.
    
* Change the Lumina On-Screen-Display to a different widget, allowing it to be shown much faster.
    
* Add new *_ifexists* functionality to any session options in :file:`luminaDesktop.conf`. This allows the distributor to more easily setup default applications, such as the web browser or 
  mail client, through an intelligent tree of options.
        
* Apply a work-around for new users which fixes a bug in Fluxbox where the virtual desktop windows could still be changed or closed by various Fluxbox keyboard shortcuts. If an existing user
  wants to apply this fix, replace their :file:`~/.lumina/fluxbox-keys` with :file:`/usr/local/share/Lumina-DE/fluxbox-keys`. Note that this will overwrite any custom keyboard shortcuts.
        
* Fix some bugs in the new window detection and adjustment routines with full-screen apps that modify the X session settings.
        
* Fix a couple bugs with the automatic detection and load routines for the new QtQuick plugins.
        
* Add in the :kbd:`Ctrl-X` keyboard shortcut for cutting items in the :ref:`Insight File Manager`.
        
* Fix up the active reloading of icons when the icon theme changes.

.. index:: changelog
.. _Lumina 0.8.5:

Lumina 0.8.5
============

* The user button has received a significant speed boost, and can now be used for browsing files and directories within the user’s home directory.
   
* Desktop icons have received a large number of changes in styling, amount of visible text, and functionality. There is also a new feature to automatically generate plugins for items in the
  user’s Desktop directory, where each plugin may be individually moved/changed rather than trapped within a container like the “desktopview” plugin.
    
* Added a desktop plugin for monitoring the system hardware status such as memory and CPU usage, CPU temperature, and disk I/O. This functionality requires operating system support
  and is currently only available for PC-BSD®, FreeBSD, and Debian.
    
* Added a desktop plugin container for running custom QtQuick/QML scripts. While there is only a single sample plugin of this type available at the present time, it is now possible for users
  to create their own custom interface plugins using the QML scripting language, which is similar to JavaScript or CSS.
  
* Lumina has been fully translated to German, Russian, and Spanish, and almost-completely translated to Catalan (89%), Chinese (61%), Estonian (53%), Indonesian (76%), Polish (89%),
  Portuguese (89%), Portuguese-Brazilian (89%), Swedish (91%), and Turkish (88%).

* The new system for desktop plugin settings requires that any desktop plugins be reset back to defaults when upgrading to this version of Lumina.

* There is a known conflict between Qt 5.4+ and Fluxbox 1.3.7 which prevents the “close” button from working on unlocked desktop plugins. To work around this issue, right-click on the title
  for the plugin and select the “close” option from the menu to remove the desktop plugin. Alternatively, you may also remove desktop plugins using the :ref:`Lumina Configuration` utility.

.. index:: changelog
.. _Lumina 0.8.4:

Lumina 0.8.4
============

* The panel has been improved to add support for mouse tracking, variable-length panels that use a percentage of the screen edge length, and the ability to pin the panel to a particular
  location on the screen edge by either corner or centered. 
  
* Rescale the panel size if the monitor used in the previous session was a different screen resolution.
  
* For hidden panels, 1% of the panel size is visible on the screen while it is hidden, rather than using a hard-coded pixel size. This is better for high-resolution screens.
    
* Remove the restriction that panels be on opposite screen edges.

* :ref:`Lumina Search` now supports the ability to change "Files or Directories" search preferences on a temporary basis. New command-line flags can be used to start searches instantly
    
* Search functionality has been integrated into the :ref:`Insight File Manager`. The :kbd:`Ctrl-F` keyboard shortcut or the “Search” menu option will start a search for a file or directory
  with the current directory as the starting point.
    
* A “Search” button has been added to the  home directory browser in the user menu. This allows the user to easily start searching for a file or directory within the selected directory.

* The new “Favorites” system backend is much faster and more reliable than the old system of symbolic links. Existing favorites should be automatically converted to the new format when you
  log into the new version of Lumina.

* The :command:`lumina-fileinfo` utility can be used to view basic file information, such as timestamps, owner/group information, file size, and read/write permissions. If the file is an XDG
  desktop shortcut that the user has permission to modify, this utility provides the ability to make changes to that shortcut by right-clicking on files in the desktop view plugin or within
  the :ref:`Insight File Manager` and selecting the “Properties” option.
  
* Better application recommendations for files and URLs, especially for web browsers or email clients.
   
* Major cleanup of XCB library usage.
    
* Hardware-brightness controls now used for PC-BSD® by default, if supported by the system hardware.
    
* Putting the system into the suspend state is now supported for PC-BSD® and Debian.
    
* New clock display formats.
    
* A large number of session cleanup and session initialization improvements, including resetting the user’s previous screen brightness and audio volume settings.
   
* New default keyboard shortcuts for tiling the open windows on the screen, on new user configurations only.

* Better support for the URL input format when required by an application.
   
* The user’s “log out” window appears much faster when activated.

* There is a known bug in Lumina 0.8.4 regarding “unlocked” desktop plugins. The close and maximize buttons for the plugin are unresponsive when using Qt 5.4.1, preventing the user from
  easily removing or maximizing a desktop plugin. As a temporary workaround, right-click the titlebar for the unlocked plugin and select close or maximize from the menu.

.. index:: changelog
.. _Lumina 0.8.3:

Lumina 0.8.3
============

* Add “Application Launcher” panel plugin which allows the user to pin the shortcut for an application directly to a panel.
   
* Add :ref:`Lumina Xconfig`, a graphical front-end to :command:`xrandr`. This utility can be used to easily enable or disable additional monitors and screens within the current desktop
  session. Shortcuts to this utility are available in the user button plugin and the settings menu plugin.
    
* Fix the issue with transparent system tray icons on FreeBSD 11.
    
* Add support for the XDG autostart specifications.

* Fix a number of bugs related to detecting and using XDG mimetypes.
    
* Add support for the XDG autostart specifications. More work is necessary to convert the current Lumina autostart specification.
     
* Add some additional fallback routines to account for possible errors in :file:`*.desktop` files.

* Add support for creating new (empty) files using :ref:`Insight File Manager`.
     
* Add an option for enabling and disabling the use of image thumbnails. This is useful if you have massive image directories, just be sure to disable thumbnails **before** loading the
  directory.
     
* Add initial drag-and-drop support for moving files and directories within a directory.
     
* Load the specific icon for any application shortcuts.
     
* Add the ability to view file checksums.
     
* Add some additional checks and excludes for copy/move operations in the background to prevent the user from performing illegal operations, such as moving a directory into itself.
     
* Add support for listing statistics about the current directory such as number of files, total size of files, and percent of the filesystem which is used.
     
* Streamline the frequency of the background directory checker so that it runs much less often.

* Disable the shutdown/restart options on PC-BSD® if the system is in the middle of performing updates in order to add an extra layer of safety.

* Have the shutdown/restart options use the “-o” option on FreeBSD and PC-BSD® so that the system performs the action much faster.
     
* Add support for thumbnails, increasing/decreasing icon sizes, removing files, and  cut/copy files to the “desktopview” desktop plugin. This plugin provides traditional desktop icons.
     
* Add support for increasing and decreasing the icon size for the application launcher desktop plugin.
     
* Update the icon used for the “favorites” system in the user button and the file manager.
     
* Add the ability to display alternate timezones in the system clock. This does **not** change the system time as it is just a setting for the visual clocks/plugins.
     
* Add a new panel plugin for pinning application shortcuts directly to the panel. This is just like the “applauncher” desktop plugin, but on the panel.
     
* Perform the initial search for applications on the system within the session initialization. This ensure that buttons and plugins are responsive as soon as the desktop becomes visible.
    
* Fix an issue with transparent system tray icons on FreeBSD 11 and convert the system tray embed/unembed routines to use the XCB library instead of XLib.
     
.. index:: changelog
.. _Lumina 0.8.2:

Lumina 0.8.2
============

* Added :command:`lumina-info` which can be used to display information about the Lumina desktop, such as the version, license, and link to the source repository.

* Large overhaul of the theme templates and color schemes which are available out-of-box.

* The :command:`lumina-config` utility has been rearranged so that its UI is more intuitive and there is a new dialog for selecting plugins. It now has the  ability to set preferred
  time and date formats and the ability to reset default applications back to their default, non-mimetype registrations.
  
* The :ref:`Insight File Manager` has been improved. All file operations happen in a separate thread so that the UI does not lag any more and the detection of Qt-editable image files
  has been fixed.
  
* Added support to update the vertical panel display of the clock plugin. Various desktop plugin stability issues have been fixed and the  session cleanup routine has been streamlined.
  A second panel is now supported and the number of filesystem watchers has been reduced to one per-session instead of one per-screen.
  
* :ref:`Lumina Search` can now be configured to exclude directories from a "Files or Directories" search and to set an alternate start directory.

.. index:: changelog
.. _Lumina 0.8.1:

Lumina 0.8.1
============

* New "Audio Player" desktop plugin to play audio files from the desktop.

* New "Home Button" panel plugin to hide all windows and show the desktop and new "Start Menu" panel plugin which provides an alternative to the user button for traditional system
  management.

* Added the ability to remove or rotate image files while viewing a slideshow with :ref:`Insight File Manager`.

* New backend distribution framework for setting system-wide defaults. This affects new users only as existing settings will not be changed. Also added the ability to
  reset the desktop back to its defaults using the :ref:`Lumina Configuration` utility.

* Allow a customizable user icon which is also used in PCDM (PC-BSD® Display Manager).

* Panels and desktop plugins follow the current theme by default.

* The "Note Pad" desktop plugin has been converted to a file-based utility so that all notes can be found in :file:`~/Notes` for access by other utilities. Plugins are
  able to load a generic text file to treat like a note for watching or updating.
  
* Auto-hidden panels now stay visible when the mouse moves over the system tray.

* The user button opens faster now as it updates the widget on-demand in the background.

* Fixed a bug in :ref:`Lumina Open` for filenames containing multiple "."s not detecting the file extension.

* The log-out window now opens on the current screen and the log-out window is hidden at the start of the log-out procedure.

.. index:: changelog
.. _Lumina 0.8.0:

Lumina 0.8.0
============

* Converted to Qt5 with XCB.

* New task manager mode which provides traditional task manager functionality.

* Task manager right-click action menu has many more options that are auto-generated based on the current window state.

* Better crash reporting through :ref:`Lumina Open`.

* Better multimedia support using the new QMultimedia framework in Qt5.

* New custom-written single-application framework with no external dependencies so it works on all operating systems.

* New windows are no longer placed underneath Lumina panels, even on multi-monitor systems.

* Special localized characters are now recognized when passed in from the command line.

* Recursive file operations now function properly in :ref:`Insight File Manager`.

* XDG "Exec" field code replacements function better, which fixes KDE application shortcuts like Okular.

.. index:: changelog
.. _Lumina 0.7.2:

Lumina 0.7.2
============

* Streamlined startup process and utilities.

* Enabled login and logout chimes.

* Added the "Note Pad" and "Desktop View" desktop plugins.

* Added the :ref:`Lumina Search` utility.

* New color schemes: Green, Gold, Purple, Red, and Glass, with Glass as the default.

* New backend system for registering default applications using mime-types instead of extensions. While all Lumina utilities have been updated to work with the new system,
  previously registered defaults might not be transferred. You may need to reset your default web browser and email client using the :ref:`Lumina Configuration` utility. 
  
.. index:: changelog
.. _Lumina 0.6.2:

Lumina 0.6.2
============

* A desktop plugin system has been implemented with two plugins: a calendar and an application launcher plugin.

* The panel plugin system has been refined with transparency support for the panel itself and automatic plugin resizing.

* Added the system dashboard panel plugin which allows control over the audio volume, screen brightness, and current workspace, while also displaying the current battery status, if
  applicable, and containing a button to let the user log out or shutdown/restart the system.
  
* The user button panel plugin has been re-implemented, incorporating the functionality of the desktopbar plugin. Now the user has quick access to files and applications in the 
  :file:`~/Desktop` folder, as well as the ability to add and remove shortcuts to system applications in the desktop folder with one click.
  
* New backgrounds wallpapers and a project logo.

* Add the :ref:`Insight File Manager`. Its features include the ability to browse the system and bookmark favorite directories. It includes a simple multimedia player for playing and
  previewing multimedia files, an image slideshow viewer for previewing image files, full file and directory restore functionality if ZFS snapshots are available, menu shortcuts to quickly
  browse attached or mounted devices, tabbing support for browsing multiple directories at once, and standard file and directory management such as copy/paste/delete/create. Supported
  multimedia and image formats are auto-detected, so if a particular file is not recognized, install the appropriate library or plugin to provide support.

* Add :ref:`Lumina Screenshot`, a simple utility to create and save screenshots. It can capture the entire system or individual windows. It can delay the image capture for a few seconds as
  necessary. This utility is automatically assigned to the “Print Screen” keyboard shortcut and is also listed in the application registry under "utilities".

* Add a new implementation of the :ref:`Lumina Configuration` utility. It can now be used to configure desktop appearance such as the background image and to add desktop plugins,
  configure the location, color, transparency, and size of panels as well as manage their plugins, with up to two panels supported per screen, configure menu plugins, manage global keyboard
  shortcuts, including shortcuts for adjusting audio volume or screen brightness, manage default applications for the system by categories or individually, manage session options such as 
  enable numlock on log in or to play audio chimes, manage applications and files to be launched on log in, and to manage window system options such as appearance, mouse focus policy,
  window placement policy, and the number of workspaces.

* Update the overall appearance of the application selector window in :ref:`Lumina Open`.

* Fully support registered mime-types on the system and recommend those applications as appropriate.

