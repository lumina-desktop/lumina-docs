.. _Introduction to Lumina:

Introduction to Lumina
**********************

The Lumina Desktop Environment (Lumina for short) is a lightweight, XDG-compliant, BSD-licensed desktop environment that focuses specifically on streamlining
the ability to get work done while minimizing system overhead. It is specifically designed for PC-BSD® and FreeBSD, but has also been ported to many other
BSD and Linux operating systems. It is based on the Qt graphical toolkit and the Fluxbox window manager, and uses a small number of X utilities for various
tasks, such as :command:`numlockx` and :command:`xscreensaver`.

Lumina's features include: 

* Very little system overhead.

* Intelligent "favorites" system for creating quick shortcuts to applications, files, and directories.

* ZFS file restore functionality through the :ref:`Insight File Manager`.

* Desktop system is plugin-based, which is similar to Android or other modern operating systems.

* Simple access to operating system-specific functionality such as screen brightness, audio volume, and battery status.

.. _User Button:

User Button
===========

Figure 1.1a shows a screenshot of Lumina on a PC-BSD® system with the "User" button clicked.

**Figure 1.1a: Lumina Desktop**

.. image:: images/lumina1.png

.. note:: while the PCDM login manager will automatically display Lumina in the desktop menu on a PC-BSD® system, users of other operating systems can add
   "Lumina-DE" as the name of the binary in their :file:`.startx`, :file:`.xinitrc`, or similar startup file.

The "User" button provides quick access for user interaction with the system. The left frame of this menu contains the following 4 tabs: 

* **Favorites:** the yellow star icon allows the user to quickly launch anything that was setup as a "favorite". Favorites can be applications, files, or
  directories, and are separated into those three categories. Favorites can be removed by clicking the small button on the right side of the entry. If the
  button icon is a red minus sign, removing the favorite does not actually delete the file as just its link is removed. If the button icon is a trash can, the
  file will actually get deleted permanently. Note that anything that exists in the users Desktop folder (:file:`~/Desktop`) is automatically treated as a
  favorite.

* **System Applications:** the white and blue gear icon lets the user browse all the applications currently registered on the system. By default, applications
  are listed alphabetically, but the list can be narrowed down by category using the drop-down list at the top of the tab. If you are running PC-BSD® or
  another operating system that has a pre-defined application "store", you will also have a shortcut at the top of the tab which will open up that application
  store. On a PC-BSD® system, the shortcut is to AppCafe®. Each application has a little "star" button on the right side of the entry. This allows
  you to mark an application as a favorite and have it appear on your personal list of quick shortcuts.

* **Home Directory:** the blue folder icon lets the user quickly browse through all the directories in their home and open any of them in the Insight file
  manager by clicking the "Browse" button. You also have the same little "star" on directories that can be clicked to mark that directory as a favorite if you
  want quick access to it later.

* **Desktop Preferences:** the yellow tool icon provides quick shortcuts to system and desktop configuration utilities. It also contains "About the Lumina Desktop"
  which can be clicked to determine the installed version of Lumina. You can also determine the version by typing :command:`lumina-info`.

If you are on PC-BSD®, or a supported operating system, you should have links to the operating system's control panel, the desktop configuration utility
(:command:`lumina-config`), :command:`qt-config` (if it is installed), the screen configuration utility (:command:`lumina-xconfig`), and the screensaver configuration utility.

Any open windows or applications will have a button appear in the section of the panel near the "User" button. If the application provides an icon, the button
will appear as that icon and if you mouse over it, the tooltip will show the name of the application. If you have multiple copies of an application running,
it will combine all those entries into a single button and list the number of windows after the icon. If you click on a button, it will automatically make
that window active. If there are multiple windows, you can select the particular window you want from a drop-down menu. The color of the button will change
depending on the state of the window: grey for a hidden or minimized window, white for a visible but inactive window, yellow for the active window, and orange
for a window that needs attention.

The system tray is located in the right portion of the panel. Any applications that register a tray icon will appear in this area. Click an icon to
interact with that application directly. The current system time shown by the clock is in the default format for the current locale.

.. index:: Lumina
.. _System Dashboard:

System Dashboard
================

The "System Dashboard" button is located at the far right of the panel and shown in Figure 1.2a. 

**Figure 1.2a: System Dashboard Menu**

.. image:: images/lumina2.png

This button provides quick access to hardware-specific information or operations, as supported by your operating system. The possible menu entries are: 

* A slider for changing the audio volume for the system from 0% to 100%. If the operating system provides a mixer utility, an icon will also appear. Click the
  icon to launch that mixer utility for advanced control of the audio system.

* The current status of the battery, if your system has one, and the estimated time remaining if that battery is discharging.

* A listing of the number of virtual workspaces that are in use, with arrows to switch between the different workspaces. 

* The "Log Out" button for ending the desktop session. When the "Log Out" button is clicked, a window of choices will be displayed in the middle of the screen.
  The choices include: "Log Out", "Restart" (if the user has permission), "Shutdown" (if the user has permission), "Cancel" (to exit the choice menu), "Lock" (which returns
  to a login menu), and "Suspend" (press the system's power button to login and resume operation).
  
.. index:: Lumina
.. _Right-Click Menu:

Right-Click Menu
================

If the user right-clicks on the desktop, a menu of quick shortcuts will appear for instant access and the title of the menu will indicate the name of the
workspace. While this menu can be customized, here is a quick summary of the default items on the menu.

* **Terminal:** used to launch a system terminal. The default is :command:`xterm`, but this can be customized.

* **Browse System:** launches the file manager. The default file manager, Insight, is recommended but this can be customized.

* **Settings:** contains configuration shortcuts for the screensaver, desktop, and screen, as well as a shortcut to Control Panel and for determining the version of Lumina.

* **Unlock/Lock Desktop:** used to lock or unlock the desktop plugins. When unlocked, desktop plugins become "active" and can be moved, resized, or removed
  from the desktop. It is recommended to leave the desktop locked during normal operations.

* **Snap Plugins to Grid:** this option only appears when the desktop is unlocked. Used to align and resize all the desktop plugins on an invisible 32x32
  pixel grid, with special adjustments to align on the bottom and right screen edges if necessary, in order to provide a uniform appearance.

* **Tile Plugins:** this option only appears when the desktop is unlocked. Used to 

* **Cascade Plugins:** this option only appears when the desktop is unlocked. Used to

* **Log Out:** opens the system log out window, with options to shutdown/restart the system (if the user has permission), log out of the desktop session, lock
  the system, or cancel the log out window.

.. index:: Lumina
.. _Lumina Configuration:

Lumina Configuration
********************

The Lumina Configuration utility, shown in Figure 2a, allows the user to configure every aspect of the desktop and is the recommended way to make changes.
To launch this utility, click the "User" icon then :menuselection:`Desktop Preferences --> Desktop Appearance/Plugins` or, right-click the desktop and click
:menuselection:`Settings --> Desktop`, or type :command:`lumina-config` from an xterm.

**Figure 2a: Lumina Desktop Configuration**

.. image:: images/lumina3.png

Each of the tabs at the top configures a different area of the system, with the most frequently changed options on the left side. Once changes have been made,
the "Save Changes" button at the bottom of the window will become active. This allows the user to setup multiple changes in any tab and apply them all at the
same time.

.. note:: if you make any changes in any of the tabs, click "Save Changes" before exiting this utility in order to save them.

The following tabs are available: 

**Appearance:** this tab is used to change the visual appearance and functionality of the desktop on a per-screen basis. The "Wallpaper" tab can be used to add
("+" button) or remove ("-" button) the image(s) to use for the desktop's wallpaper. By default, when you click the "+" button, the Lumina backgrounds stored in
:file:`/usr/local/share/wallpapers/Lumina-DE/` are displayed. Click the drop-down "Look In:" menu to select an alternate wallpaper location. If multiple images
are selected, the "Rotate Background" button can be selected as well as a specified time interval in minutes to rotate to the next image.

Click the "Theme" tab to change the default font, font size, theme template, color scheme, and icon pack. It is possible to create your own theme template or color
scheme by clicking the "Edit" button next to those options and changing the settings as necessary. Note that the theme templates are written as Qt stylesheets, so some
scripting experience may be helpful when configuring a theme. After making your changes, you can either click the "Save" button to save the theme without closing the editor,
or click the "Apply" button which will both save the theme and close the theme editor.

**Interface:** the "Interface" tab is used to configure the desktop menu and panels. Its "Desktop" tab, shown in Figure 2b, is used to configure which items appear in the
right-click menu.

**Figure 2b: Right-Click Menu Configuration**

.. image:: images/lumina4.png

To add an item to the right-click menu, click the "+" button. This will open the "Select Plugin" where you can add an application, custom app, an entry for the File Manager,
a separator, a shortcut to Settings, a terminal, or a listing of currently open applications. Alternately, click "Add Utility to Screen" and select which application to add.
To remove an item from the right-click menu, highlight it and click the "-" button. Use the arrow buttons to change the order of the items in the right-click menu.

Click the "Panels" tab to see the screen shown in Figure 2c.

**Figure 2c: Panel Configuration**

.. image:: images/lumina5a.png

This screen can be used to customize the location, size, alignment, and theme of an existing panel and to add ("+") or delete ("-") additional panels. Panels must
be aligned along a screen edge, opposite screen edges in the case of two panels, and may have any width, color, or transparency. Use the "Location" drop-down menu
to set the location of the panel which can be "Top", "Bottom", "Left", or "Right". The "Alignment" drop-down menu can be used to center the panel on the edge or pin it
to one of the corners. The "Size" can be used to specify the panel width in pixels and the length as a percentage. If you would like the panel to be hidden unless
the mouse is hovered over it, click "Appearance" then check the "Auto-hide Panel" box. The "Custom Color" option in the "Appearance" screen can be used to fine-tune the
panel color. 

Once a panel's appearance has been configured, plugins can be added by clicking "Plugins" then the "+" button and selecting a plugin from the list that appears. Similarly,
clicking the "-" button will remove the selected plugin, and the arrow buttons can be used to move the location of the plugin on the panel. The top of the
list corresponds to either the top of a vertical panel or the left side of a horizontal panel. Some of the available plugins include:

* Application Launcher: when you select this plugin, it will prompt you to select the application to launch. This will add a shortcut for launching the selected application
  to the panel.

* Battery Monitor: hover over this icon to view the current charge status of the battery. When the charge reaches 15% or below, the low battery icon will flash intermittently
  and will change to a low battery icon when there is less than 5% charge left.

* Desktop Bar: adds a "star" button for automatically displaying entries for anything in the :file:`~/Desktop` folder and alternately launching the selected entry.

* Desktop Switcher: used to switch between virtual desktops.

* Home Button: this button will hide all open windows so that only the desktop is visible. This is useful for touch screens or small devices.

* Start Menu: adds a classic start menu as seen on other operating systems.

* System Dashboard: used to view/modify audio volume, screen brightness, batterly life, and virtual desktops.

* System Tray: provides a display area for dockable applications.

* Task Manager: is added by default. Its behavior is to group windows by application.

* Task Manager (No Groups): ensures that every window gets its own button. This uses a lot more space on the panel since it needs to put part of the window title on
  each button.

* Time/Date: displays the current time and date.

* User Button: main button for accessing applications, directories, settings, and log out.

.. note:: each Lumina plugin automatically contains a unique settings file in :file:`~/.lumina/desktop-plugins/<plugin_name>---<screen number>.<pluginnumber>.conf`, which
   contains its location and sizing information as well as providing the possibility for each plugin to store its own customized settings as necessary.

**Applications:** the "Applications" tab, shown in Figure 2d, is used to configure which applications start when you login to Lumina as well as the default
applications and file types.

**Figure 2d: Lumina Applications Configuration**

.. image:: images/lumina6a.png

To prevent an application from starting automatically, uncheck its box.

To add an application to the auto-start configuration , click "Application" to select the application's name from a drop-down menu or click "Binary" or "File" to browse
to the location of  the application or file to open. If you select a file name, Lumina will automatically open it in an application that is capable of reading the file type.

To configure the default applications and file types, click the "File Defaults" tab. In the screen shown in Figure 2e, you can configure the default web browser,
email client, file manager, and virtual terminal. Either click "Click to Set" or the name of the existing application to select from a menu of available applications.
If you wish to restore the default application, click the current application's name, then click "Restore Defaults".

**Figure 2e: Lumina Defaults Configuration**

.. image:: images/lumina7a.png

This screen can also be used to set the default application for several categories of file types. To add an application, select the file type and either
click "Set App", which will open a drop-down menu of common applications, or "Set Binary", which will open a file browser so that you can browse to the path
of the application.

.. note:: some applications, such as web browsers, keep their own internal lists of default applications for opening particular types of files. If you set
   that application to use the :command:`lumina-open` or :command:`xdg-open` utilities, it will use the default applications that are set here instead so that
   there is only a single list of default applications for the system.

**Shortcuts:** the "Shortcuts" tab, shown in Figure 2f, is used to configure various keyboard shortcuts for system or window tasks. Most of these
options relate to window and workspace management, such as moving windows between workspaces, but there are also options for changing the system audio volume
or screen brightness. Note that a shortcut that is already in use can **not** be assigned to another action. First, that shortcut needs to be cleared and
saved, before that key press will be detectable when creating or changing a shortcut.

**Figure 2f: Lumina Shortcuts Configuration**

.. image:: images/lumina8.png

**Session:** the "Session" tab, shown in Figure 2g, governs the general settings for the desktop session. These settings are usually not changed on a
frequent basis.

**Figure 2g: Lumina Session Configuration**

.. image:: images/lumina12a.png

The "General Options" tab contains the following options: "Enable numlock on startup", "Play chimes on startup", and "Play chimes on exit". It can also
be used to change the user's icon which appears in the login menu and to set the time format, date format, and time zone. It can also be used to reset
the desktop settings to either system defaults or Lumina defaults.

The "Window System" tab allows the user to setup various configuration options for the window manager. These options include the number of workspaces,
where new windows are placed on the screen, when windows receive focus, and the appearance of the frame around application windows.

.. index:: Utilities
.. _Lumina Utilities:

Lumina Utilities
****************

Lumina provides many built-in utilities, which are described in this chapter.

.. index:: Lumina
.. _Lumina Screenshot:

Lumina Screenshot
=================

This utility can be used to take screenshots of the desktop or applications and save them as PNG image files. To launch this utility, click the icon for
:menuselection:`System Applications --> Lumina Screenshot` or type :command:`lumina-screenshot` from an xterm.

To take a screenshot, click the "Snap" button in the upper-right corner of the screen shown in Figure 3.1a.

**Figure 3.1a: Lumina Screenshot**

.. image:: images/lumina9.png

The settings at the bottom of the window can be used to select the "Entire Screen" or to "Select Window". The delay, in number of seconds, can also be
configured in order to give time to setup the screenshot. If you like the look of the taken screenshot, as shown in the preview, click the "Save" button to
open a window where you can specify the name and location of the saved screenshot.

.. note:: the "Print Screen" keyboard shortcut is set to run this utility by default.

.. index:: Lumina
.. _Insight File Manager:

Insight File Manager
====================

The Insight file manager, shown in Figure 3.2a, allows the user to easily browse and modify files on the local system on a per-directory basis. To open
Insight, right-click the desktop and select "Browse System" or type :command:`lumina-fm` from an xterm.

**Figure 3.2a: Insight File Manager**

.. image:: images/lumina10.png

It is possible to open up additional directories through the tab system using :kbd:`Ctrl-T` or click :menuselection:`File --> New Tab`, allowing the user to
easily manage multiple locations on the system. Insight also features the ability to "bookmark" locations on the system for instant access via the "star"
button. Once a location has been bookmarked, it will be available via the "Bookmarks" menu at the top of the window. Any removable devices that are available
on the system will show up in the "External Devices" menu, if supported by the operating system. When an item is selected, the options on the left side of the
screen will show the possible actions that may be taken with regards to that item. Possible actions include: "open", "open with" (will prompt for the
application to use), "add to favorites", "rename", "cut", "copy", "paste", and "delete". By default, the actions buttons are visible. They can be made
invisible by clicking :menuselection:`View --> Show Action Buttons`. To disable thumbnails, uncheck :menuselection:`View --> Load Thumbnails`. Note that
this option does not retroactively remove thumbnails that have already been loaded, it only prevents loading thumbnails in new directories. Hidden files are
not shown by default; this can be changed by checking :menuselection:`View --> Show Hidden Files`.

If you select a file or directory and right-click it, the following options become available: "Open", "Open With" (where you select the application to use), "Rename",
"View Checksums" (shows the MD5 checksum), "Cut Selection", "Copy Selection", "Paste", "Delete Selection", or "File Properties" (such as file type, size,
permissions, and creation date).

A few additional options may be available at the bottom of the window, depending on the directory being viewed and the types of files that are in it:

* **New file:** the ability to create a new file is available if the user has permission to modify the contents of the current directory.

* **New Dir:** the ability to create a new directory is available if the user has permission to modify the contents of the current directory.

* **Slideshow:** if there are image files in the directory, this option will display those image files as a slideshow and provide arrows for going forward or back by
  one file or to the very beginning or end of the file list. Buttons are also provided for deleting the currently displayed image or to rotate it, and save the
  rotation, clockwise or counter-clockwise.

* **Play:** will appear if there are supported multimedia files in the directory. The types of files that are supported depends on what multimedia plugins are
  installed on the system. If a particular file is not recognized as a multimedia file, install the associated multimedia codec using the operating system's
  application management software and restart the file manager.

* **Backups:** if the system is formatted with ZFS and snapshots of the current directory are available, this button will appear. Snapshots are organized from
  oldest to newest, with the most recent snapshot selected by default, and the contents of the directory at the time of that snapshot are displayed. To
  restore a file or multiple files, select them from the list and click the "Restore Selection" button. If those files still exist and you want to overwrite
  them, make sure the "Overwrite Existing Files" option is checked first. Otherwise, if a file with that name exists, the restore will append a number to the
  end of the filename. For example, the first restored version of :file:`testfile.txt` will become :file:`testfile-1.txt`.
  
.. index:: Lumina
.. _Lumina Open:

Lumina Open
===========

To open a file, directory, or URL from the command line, use :command:`lumina-open` followed by the full path to the file or the URL. This utility will look
for an appropriate application to use to open the specified file or URL. If there is no default application registered for the input type, a small dialog will
prompt the user to select which application to use, and optionally set it as the default application for this file type. As seen in Figure 3.3a, this dialog
organizes the available applications into three types: 

* **Preferred:** these applications have registered their Mime type with the system and can open that type of file. Also included are any applications that
  have been used to open this type of file before as it keeps track of the last three applications used for that file type.

* **Available:** displays all the applications installed on the system, organized by category and name.

* **Custom:** lets the user manually type in the binary name or path of the application to use. It also provides a small button to let the user graphically
  search the system for the binary. Whenever text is entered, a check is performed to determine whether that is a valid binary and the icon will change
  between a green checkmark or a red X as appropriate.

**Figure 3.3a: Lumina Open**

.. image:: images/lumina11.png

.. index:: Lumina
.. _Lumina Search:

Lumina Search
=============

The :command:`lumina-search` utility provides the ability to easily search for and launch applications or to quickly search for file and directories. The "*" wildcard
can be used in the search terms and the search will include hidden files if the search term starts with a dot ("."). Figure 3.4a shows a screenshot of this utility.

**Figure 3.4a: Lumina Search**

.. image:: images/lumina13.png

By default, a "Files or Directories" search is limited to the user's home directory, as indicated by the "Search: ~" at the bottom of the screen. The "Smart: Off" indicates
that every subdirectory is included in the search; in other words, there are no excluded directories. To add additional search directories or to exclude subdirectories, click 
the wrench icon to see the screen shown in Figure 3.4b.

**Figure 3.4b: Configuring the Search Directories**

.. image:: images/lumina14.png

Click the blue folder icon to change the starting search directory. For example, you can select "Computer" then "/" from the "Select Search Directory" screen to search the entire
contents of the computer. You can also add directories to exclude from searches by clicking the "+" button. If you add any excludes, you can delete an exclude by highlighting it
and clicking the "-" button. By default, the "Save as Defaults" option is selected. Unselect this option if you only wish to temporarily modify your search settings.

.. index:: Lumina
.. _Lumina Xconfig:

Lumina Xconfig
==============

The :command:`lumina-xconfig` utility is a graphical front-end to the :command:`xrandr` command line utility. It provides the ability to probe and manage any number
of attached monitors. To start this utility, right-click the desktop and select :menuselection:`Settings --> Screen Configuration`, click the "User" icon then
:menuselection:`Desktop Preferences --> Screen Configuration`, or type :command:`lumina-xconfig` from an xterm. This will open a screen similar to the one shown in
Figure 3.5a.

**Figure 3.5a: Configuring Monitors**

.. image:: images/lumina15.png

In this example, two monitors are attached to the system and each is displayed along with their current screen resolution.

.. _How to Get Lumina:

How to Get Lumina
*****************

Lumina is available as a pre-built package for the following operating systems. Click the hyperlink for instructions on how to install the Lumina package on that operating system.

* `Arch Linux AUR <http://lumina-desktop.org/get-lumina/#arch>`_

* `Debian 8 “Jessie” <http://lumina-desktop.org/get-lumina/#debian>`_

* `Debian Testing “Stretch” and Debian Unstable “Sid” <http://lumina-desktop.org/get-lumina/#debian-testing>`_

* `FreeBSD <http://lumina-desktop.org/get-lumina/#freebsd>`_

* `OpenBSD <http://lumina-desktop.org/get-lumina/#openbsd>`_

* `PC-BSD <http://lumina-desktop.org/get-lumina/#pcbsd>`_

In addition to pre-built packages, the `Lumina source repository <https://github.com/pcbsd/lumina>`_ is available on GitHub so that developers can contribute code or create
packages for other distributions. If you plan to compile Lumina from source, refer to `DEPENDENCIES <https://github.com/pcbsd/lumina/blob/master/DEPENDENCIES>`_ and ensure all
dependent software is installed and to `README <https://github.com/pcbsd/lumina/blob/master/README.md>`_ for build instructions.

.. _Contributing to Lumina:

Contributing to Lumina
**********************

.. _Reporting Bugs:

Reporting Bugs
==============

.. _Localization and Translations:

Localization and Translations
=============================


