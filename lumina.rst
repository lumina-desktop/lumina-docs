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

.. _How to Get Lumina:

How to Get Lumina
*****************

Lumina is available as a pre-built package for the following operating systems. Click the hyperlink for instructions on how to install the Lumina package on that operating system.

* `Arch Linux AUR <http://lumina-desktop.org/get-lumina/#arch>`_

* `Debian 8 “Jessie” <http://lumina-desktop.org/get-lumina/#debian>`_

* `Debian Testing “Stretch” and Debian Unstable “Sid” <http://lumina-desktop.org/get-lumina/#debian-testing>`_

* `Fedora 22 <http://lumina-desktop.org/get-lumina/#fedora>`_

* `FreeBSD <http://lumina-desktop.org/get-lumina/#freebsd>`_

* `Manjaro Linux <http://lumina-desktop.org/get-lumina/#manjaro>`_

* `OpenBSD <http://lumina-desktop.org/get-lumina/#openbsd>`_

* `PC-BSD <http://lumina-desktop.org/get-lumina/#pcbsd>`_

* `Slackware <http://lumina-desktop.org/get-lumina/#slackware>`_

In addition to pre-built packages, the `Lumina source repository <https://github.com/pcbsd/lumina>`_ is available on GitHub so that developers can contribute code or create
packages for other distributions. If you plan to compile Lumina from source, refer to `DEPENDENCIES <https://github.com/pcbsd/lumina/blob/master/DEPENDENCIES>`_ and ensure all
dependent software is installed and to `README <https://github.com/pcbsd/lumina/blob/master/README.md>`_ for build instructions.

Once installed, add "Lumina-DE" as the name of the binary in your :file:`.startx`, :file:`.xinitrc`, or similar X startup file.

.. note:: No startup configuration is needed when installed on a PC-BSD® system as the PCDM login manager will automatically display Lumina in the login menu. Simply log out, select Lumina,
   and log back in.
   
The rest of this Handbook describes the Lumina Configuration utility and the various utilities which are built into Lumina. It then describes how you can contribute to the Lumina Project and
lists the changelogs for each version of Lumina.

.. _Introduction to Lumina:

Introduction to Lumina
**********************

:numref:`Figure %s: Lumina Desktop <lumina1b>` shows a screenshot of Lumina on a PC-BSD® system with the "User" button clicked.

.. _lumina1b:

.. figure:: images/lumina1b.png

The "User" button provides quick access for user interaction with the system. The left frame of this menu contains the following 4 tabs: 

* **Favorites:** the yellow star on a blue folder icon can be used to quickly launch anything that was setup as a "favorite". Favorites can be applications, files, or
  directories, and are separated into those three categories. Favorites can be removed by clicking the icon on the right side of the entry. If the
  icon is a red minus sign, removing the favorite does not actually delete the file as just its link is removed. If the button icon is a trash can, the
  file will actually get deleted permanently. Note that anything that exists in the users Desktop folder (:file:`~/Desktop`) is automatically treated as a
  favorite.

* **Applications:** the white and blue gear icon lets the user browse all the applications currently registered on the system. By default, applications
  are listed alphabetically, but the list can be narrowed down by category using the drop-down list at the top of the tab. If you are running PC-BSD® or
  another operating system that has a pre-defined application store, you will also have a shortcut at the top of the tab which will open up that application
  store. On a PC-BSD® system, the shortcut is to AppCafe®. Any application that is not currently marked as a favorite has a "star" button on the right side of the entry. This allows
  you to add an application to "Favorites".

* **Home Directory:** the blue folder icon can be used to browse through all the directories in their home and open any of them in the :ref:`Insight File Manager`. Click the star icon
  to the right of the directory name to add it to "Favorites".

* **Desktop Preferences:** the tool icon provides quick shortcuts to system and desktop configuration utilities. It also contains "About the Lumina Desktop" which can be clicked to
  determine the installed version of Lumina. You can also determine the version by typing :command:`lumina-info`. If you are on PC-BSD®, or an operating system which provides the following
  features, this section will contain links to the operating system's control panel, the desktop configuration utility (:command:`lumina-config`), :command:`qt-config` (if it is installed),
  the screen configuration utility (:command:`lumina-xconfig`), and the screensaver configuration utility.

Any open windows or applications will have a button appear in the section of the panel near the "User" button. If the application provides an icon, the button
will appear as that icon and if you mouse over it, the tooltip will show the name of the application. If you have multiple copies of an application running,
it will combine all those entries into a single button and list the number of windows after the icon. If you click on a button, it will automatically make
that window active. If there are multiple windows, you can select the particular window you want from a drop-down menu. The color of the button will change
depending on the state of the window: grey for a hidden or minimized window, white for a visible but inactive window, yellow for the active window, and orange
for a window that needs attention.

The system tray is located in the right portion of the panel. Any applications that register a tray icon will appear in this area. Click an icon to
interact with that application directly. The current system time shown by the clock is in the default format for the current locale.

.. index:: dashboard
.. _System Dashboard:

System Dashboard
================

The "System Dashboard" button is located at the far right of the panel. If you click this icon, you will see a menu similar to that shown in
:numref:`Figure %s: System Dashboard Menu <lumina2a>`.

.. _lumina2a:

.. figure:: images/lumina2b.png

This button provides quick access to hardware-specific information or operations, as supported by your operating system. The possible menu entries are: 

* **System Volume:** a slider for changing the system audio volume from 0% to 100%. If the operating system provides a mixer utility, an icon will also appear. Click the
  icon to launch that mixer utility for advanced control of the audio system.

* **Screen Brightness:** a slider for changing the screen brightness from 0% to 100%.

* **Battery Status:** the current status of the battery, if your system has one, and the estimated time remaining if that battery is discharging.

* **Workspace:** a listing of the number of virtual workspaces that are in use, with arrows to switch between the different workspaces. 

* **Locale:** this will only appear if the lumina-i18n package is installed. The current locale will be displayed as the title of the drop-down menu. Click the drop-down menu to select
  another locale for this session. Refer to :ref:`Session` for more information on fine-tuning the locale settings.

* **Log Out:** when this button is clicked, a window of choices will be displayed in the middle of the screen.
  The choices include: "Log Out", "Restart" (if the user has permission), "Shutdown" (if the user has permission), "Cancel" (to exit the choice menu), "Lock" (which returns
  to a login menu), and, if the operating system supports it, "Suspend" (press the system's power button to login and resume operation).
  
.. index:: right-click menu
.. _Right-Click Menu:

Right-Click Menu
================

If the user right-clicks on the desktop, a menu of quick shortcuts will appear and the title of the menu will indicate the name of the
workspace. While this menu can be customized, here is a quick summary of the default items on the menu:

* **Terminal:** used to launch a system terminal. The default is :command:`xterm`, but this can be customized.

* **Browse System:** launches the file manager. The default file manager, Insight, is recommended but this can be customized.

* **Applications:** provides shortcuts to the user's home directory, the operating system's graphical software management utility (if available), the control panel (if the operating
  system provides one), and the applications currently registered on the system, arranged by system category.

* **Settings:** contains shortcuts to the screensaver preferences, :ref:`Lumina Configuration` utility, screen configuration (:ref:`Lumina Xconfig`), the operating
  system's control panel, and for determining the version of Lumina.

* **Log Out:** opens the system log out window, with options to shutdown/restart the system (if the user has permission), log out of the desktop session, lock
  the system, cancel the log out window, or suspend the system (if the operating system supports suspend mode).

.. index:: configuration
.. _Lumina Configuration:

Lumina Configuration
********************

The Lumina Configuration utility, shown in :numref:`Figure %s: Lumina Desktop Configuration <lumina3a>`, can be used to configure every aspect of the desktop and is the recommended way to
make changes. To launch this utility, click the "User" icon then :menuselection:`Desktop Preferences --> Desktop Appearance/Plugins`, right-click the desktop and click
:menuselection:`Settings --> Desktop`, or type :command:`lumina-config` from an xterm.

.. _lumina3a:

.. figure:: images/lumina3a.png

Each of the tabs at the top configures a different area of the system, with the most frequently changed options on the left side. As changes are made,
the "Save Changes" button at the bottom of the window becomes active. This allows the user to setup multiple changes in any tab and apply them all at the
same time.

.. note:: If you make any changes in any of the tabs, remember to click "Save Changes" before exiting this utility in order to save them.

The rest of this section describes the configurations that are available in each tab. 

.. index:: appearance, wallpaper
.. _Appearance:

Appearance
==========

This tab is used to change the visual appearance and functionality of the desktop on a per-screen basis. The "Wallpaper" tab, shown in
:numref:`Figure %s: Lumina Desktop Configuration <lumina3a>`, can be used to add a wallpaper ("+" button), create a color to use as a wallpaper (paint button), or remove ("-" button) a
wallpaper. By default, when you click the "+" button, the Lumina backgrounds stored in :file:`/usr/local/share/wallpapers/Lumina-DE/` are displayed. Click the drop-down "Look In:" menu to
select an alternate wallpaper location. If multiple images are selected, the "Rotate Background" button can be selected as well as a specified time interval in minutes to rotate to the next
image. 

The options that are available when you click the paint icon are shown in :numref:`Figure %s: Modifying the Wallpaper <lumina16>`. If you select a color and click "OK", it will be added as a
solid color background to the wallpaper selection drop-down menu.

.. _lumina16:

.. figure:: images/lumina16.png

The "Theme" tab, shown in :numref:`Figure %s: Modifying the Theme <lumina17a>`, can be used to change the default font, font size, theme template, color scheme, and icon pack. 

.. _lumina17a:

.. figure:: images/lumina17a.png

It is possible to create your own "Theme Template" or "Color Scheme" by clicking the "Edit" button next to those options and changing the settings as necessary.
:numref:`Figure %s: Using the Theme Editor <lumina18>` shows an example of clicking the "Edit" button with the "Lumina-default (System)" theme template selected. This action opened the
"Theme Editor" and the user has clicked the color selector icon (dropper) in the upper right corner. After selecting an item in this menu, the template controlling that selection can be
edited by changing the values in the theme editor box. Note that the theme templates are written as `Qt stylesheets <http://doc.qt.io/qt-5/stylesheet.html>`_, so some scripting experience
may be helpful when configuring a theme. After making your changes, you can either click the "Save" button to save the theme without closing the editor, or click the "Apply" button which
will both save the theme and close the theme editor.

.. _lumina18:

.. figure:: images/lumina18.png

.. index:: menu, panel
.. _Interface:

Interface
=========

The "Interface" tab is used to configure the desktop menu and panels. Its "Desktop" tab, shown in :numref:`Figure %s: Right-Click Menu Configuration <lumina4b>`, is used to configure which
items appear in the right-click menu and which items are embedded onto the desktop.

.. _lumina4b:

.. figure:: images/lumina4b.png

To add an item to the right-click menu, click the "+" button under the "Quick-Access Menu". This will open the "Select Plugin" screen where you can add an application, custom app, an entry
for the File Manager, a separator, a shortcut to Settings, a terminal, or a listing of currently open applications. To remove an item from the right-click menu, highlight it and click the
"-" button. Use the arrow buttons to change the order of the items in the right-click menu.

To embed a utility onto the desktop, click the "+" button under the "Embedded Utilities" frame. Currently, the following plugins can be added as an icon on the desktop: Application Launcher
(opens a menu listing which applications can be launched), Audio Player, Calendar, Desktop Icons View, Note Pad, Sample, and System Monitor. Once you click the "Save Changes" button, any
utilities you added will appear on top of the desktop. To remove an embedded utility from the desktop, highlight its entry under "Embedded Utilities", click the "-" button, and click "Save
Changes". Alternately, right-click the icon for the utility and select "Close" from the right-click menu.

.. note:: At this time, it is a known bug that the "x" in the upper right corner of an embedded utility will not remove that utility from the desktop. To bypass this bug, either right-click
   the name of the utility and select "Close" from the right-click menu or use the "-" button under "Embedded Utilities" as described above.

The "Generate Desktop Links" option is used to display each item stored in :file:`~/Desktop` as an icon on the desktop. By default, this option is selected as its box is black. If you
de-select this option and click "Save Changes", the icons for the contents of :file:`~/Desktop` will be removed from the desktop.
   
To configure the panel, click the "Panels" tab which will open the screen shown in :numref:`Figure %s: Panel Location Tab <lumina5b>`.

.. _lumina5b:

.. figure:: images/lumina5b.png

This screen can be used to customize the location, alignment, size, theme, and plugins for an existing panel, as well as to add ("+"), customize, or delete ("-") additional panels. Panels
must be aligned along a screen edge, opposite screen edges in the case of two panels, and may have any width, color, or transparency. 

The "Location" tab contains the following items:

* **Edge:** this drop-down menu can be used to set the location of the panel which can be "Top", "Bottom", "Left", or "Right". 

* **Alignment:** this drop-down menu can be used to center the panel on the edge or pin it to one of the corners. 

* **Size:** can be used to specify the panel width in pixels. 

The "Appearance" tab is shown in :numref:`Figure %s: Panel Appearance Tab <lumina19>`.

.. _lumina19:

.. figure:: images/lumina19.png

If you would like the panel to be hidden unless the mouse is hovered over it, check the "Auto-hide Panel" box. The "Custom Color" option can be used to fine-tune the
panel color. Click its box, then the paint icon to select the panel color.

The "Plugins" tab is shown in :numref:`Figure %s: Panel Plugins Tab <lumina20>`.

.. _lumina20:

.. figure:: images/lumina20.png

To add a plugin as an icon to the panel, click the "+" button and select a plugin from the list that appears. To remove a plugin, highlight it and
click the "-" button. The arrow buttons can be used to move the location of the plugin on the panel. The top of the list corresponds to either the top of a vertical panel or the left side
of a horizontal panel. The available plugins include:

* **Application Launcher:** when you select this plugin, it will prompt you to select the application to launch. This will add a shortcut for launching the selected application
  to the panel.
  
* **Application Menu:**

* **Battery Monitor:** hover over this icon to view the current charge status of the battery. When the charge reaches 15% or below, the low battery icon will flash intermittently
  and will change to a low battery icon when there is less than 5% charge left.

* **Desktop Bar:** adds a "star" button for automatically displaying entries for anything in the :file:`~/Desktop` folder and alternately launching the selected entry.

* **Show Desktop:** this button will hide all open windows so that only the desktop is visible. This is useful for touch screens or small devices.

* **Spacer:** adds a blank area to the panel.

* **Start Menu:** adds a classic start menu as seen on other operating systems.

* **System Dashboard:** used to view/modify audio volume, screen brightness, battery life, and virtual desktops.

* **System Tray:** provides a display area for dockable applications.

* **Task Manager (No Groups):** ensures that every window gets its own button. This uses a lot more space on the panel since it needs to put part of the window title on
  each button.
  
* **Task Manager:** is added by default. Its behavior is to group windows by application.

* **Time/Date:** displays the current time and date.

* **User Button:** main button for accessing applications, directories, settings, and log out.

* **Workspace Switcher:** used to switch between virtual desktops.

.. note:: Each Lumina plugin automatically contains a unique settings file in :file:`~/.lumina/desktop-plugins/<plugin_name>---<screen number>.<pluginnumber>.conf`, which
   contains its location and sizing information as well as providing the possibility for each plugin to store its own customized settings as necessary.

.. index:: application startup
.. _Applications:

Applications
============

The "Applications" tab, shown in :numref:`Figure %s: Lumina Applications Configuration <lumina6a>`, is used to configure which applications start when you login to Lumina as well as the
default applications and file types.

.. _lumina6a:

.. figure:: images/lumina6a.png

To prevent an application from starting automatically, uncheck its box.

To add an application to the auto-start configuration , click "Application" to select the application's name from a drop-down menu or click "Binary" or "File" to browse
to the location of  the application or file to open. If you select a file name, Lumina will automatically open it in an application that is capable of reading the file type.

To configure the default applications and file types, click the "File Defaults" tab. In the screen shown in :numref:`Figure %s: Lumina Defaults Configuration <lumina7b>`, you can configure
the default web browser, email client, file manager, and virtual terminal. 

.. _lumina7b:

.. figure:: images/lumina7b.png

Click the gear icon or the name of the existing application to select the desired application from a menu of available applications.
If you wish to go back to the default application, click the current application's name, then click "Restore Defaults".

This screen can also be used to set the default application for several categories of file types. To add an application, select the file type and either
click "Set App", which will open a drop-down menu of common applications, or "Set Binary", which will open a file browser so that you can browse to the path
of the application.

.. note:: Some applications, such as web browsers, keep their own internal lists of default applications for opening particular types of files. If you set
   that application to use the :command:`lumina-open` or :command:`xdg-open` utilities, it will use the default applications that are set here instead so that
   there is only a single list of default applications for the system.

.. index:: shortcuts
.. _Shortcuts:

Shortcuts
=========
   
The "Shortcuts" tab, shown in :numref:`Figure %s: Lumina Shortcuts Configuration <lumina8>`, is used to configure various keyboard shortcuts for system or window tasks. Most of these
options relate to window and workspace management, such as moving windows between workspaces, but there are also options for changing the system audio volume
or screen brightness. Note that a shortcut that is already in use can **not** be assigned to another action. First, that shortcut needs to be cleared and
saved, before that key press will be detectable when creating or changing a shortcut.

.. _lumina8:

.. figure:: images/lumina8.png

.. index:: session
.. _Session:

Session
=======

The "Session" tab, shown in :numref:`Figure %s: Session General Options Tab <lumina12c>`, governs the general settings for the desktop session. These settings are usually not changed on a
frequent basis.

.. _lumina12c:

.. figure:: images/lumina12c.png

The "General Options" tab can be used to automatically enable numlock, to play chimes when Lumina starts or exits, and to change the icon that appears  in the login menu and the "User"
button. It also has options to set the time format, date format, time zone, and time display. Buttons are available to reset these options
to either system defaults or Lumina defaults.

The "Locale" tab is shown in :numref:`Figure %s: Session Locale Tab <lumina21>`.

.. _lumina21:

.. figure:: images/lumina21.png

The lumina-i18n package provides localization files. Once installed, this allows you to customize which locale is used for the various items listed in
:numref:`Figure %s: Session Locale Tab <lumina21>`. To install this package on a PC-BSD or FreeBSD system, use :command:`sudo pkg install lumina-i18n`. On other operating systems, use the
software management tool that comes with the operating system. If the Lumina Configuration utility was open before the installation, restart it so that the list of localizations can be
loaded into the drop-down menus of this screen. Since each setting has its own drop-down menu, you have the flexibility to select different locales for each item shown in this screen. Note
that if you make any changes in the "Locale" tab, click the "Save Changes" button and restart Lumina so that the configured locales can be loaded.

Installing the lumina-i18n package will also add a drop-down menu to the system dashboard menu shown in :numref:`Figure %s: System Dashboard Menu <lumina2a>`. Note that you need to restart
Lumina after the package installation in order for this option to be added to the dashboard menu. This drop-down menu can be used to temporarily change the locale for this session only. This
will immediately change the localization of any translated menu items on the fly so that you do not have to log back into the Lumina session.

.. note:: Any menu items that continue to be displayed in English have not been translated to the selected language yet. You can assist the Lumina Project in translating menu items using the
   instructions in :ref:`Interface Translation`.

The "Window System" tab, shown in :numref:`Figure %s: Session Window System Tab <lumina22>`, contains various configuration options for the window manager. 

.. _lumina22:

.. figure:: images/lumina22.png

Drop-down menus are provided for configuring the following:

* **Number of Workspaces:** up to *10* workspaces can be defined, with a default of
  *2*.

* **New Window Placement:** indicates where new windows are placed on the screen. Choices are "Align in a Row", "Align in a Column", "Cascade", or "Underneath Mouse".

* **Focus Policy:** indicates when windows receive focus. Choices are "Click to Focus", "Active Mouse Focus", or "Strict Mouse Focus".

* **Window Theme:** controls the appearance of the frame around application windows. The "Window Theme Preview" screen can be used to preview the selected theme.

.. index:: Utilities
.. _Lumina Utilities:

Lumina Utilities
****************

Lumina provides many built-in utilities, which are described in this chapter.

.. index:: screenshot
.. _Lumina Screenshot:

Lumina Screenshot
=================

This utility can be used to take screenshots of the desktop or applications and save them as PNG image files. To launch this utility, click the icon for
:menuselection:`Applications --> Lumina Screenshot` or type :command:`lumina-screenshot` from an xterm.

To take a screenshot, click the "Snap" button in the upper-right corner of the screen shown in :numref:`Figure %s: Lumina Screenshot <lumina9a>`.

.. _lumina9a:

.. figure:: images/lumina9a.png

The settings at the bottom of the window can be used to select the "Entire Screen" or to "Select Window". The delay, in number of seconds, can also be
configured in order to give time to setup the screenshot. If you like the look of the taken screenshot, as shown in the preview, click the "Save" button to
open a window where you can specify the name and location of the saved screenshot.

.. note:: The "Print Screen" keyboard shortcut is set to run this utility by default.

.. index:: file manager
.. _Insight File Manager:

Insight File Manager
====================

The Insight file manager, shown in :numref:`Figure %s: Insight File Manager <lumina10>`, allows the user to easily browse and modify files on the local system on a per-directory basis. To
open Insight, right-click the desktop and select "Browse System" or type :command:`lumina-fm` from an xterm.

.. _lumina10:

.. figure:: images/lumina10.png

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
  
.. index:: application launcher
.. _Lumina Open:

Lumina Open
===========

To open a file, directory, or URL from the command line, use :command:`lumina-open` followed by the full path to the file or the URL. This utility will look
for an appropriate application to use to open the specified file or URL. If there is no default application registered for the input type, a small dialog will
prompt the user to select which application to use, and optionally set it as the default application for this file type. As seen in the example shown in
:numref:`Figure %s: Lumina Open <lumina11a>`, this dialog organizes the available applications into three types: 

* **Preferred:** these applications have registered their Mime type with the system and can open that type of file. Also included are any applications that
  have been used to open this type of file before as it keeps track of the last three applications used for that file type.

* **Available:** displays all the applications installed on the system, organized by category and name.

* **Custom:** lets the user manually type in the binary name or path of the application to use. It also provides a small button to let the user graphically
  search the system for the binary. Whenever text is entered, a check is performed to determine whether that is a valid binary and the icon will change
  between a green checkmark or a red X as appropriate.

.. _lumina11a:

.. figure:: images/lumina11a.png

.. index:: search
.. _Lumina Search:

Lumina Search
=============

The :command:`lumina-search` utility provides the ability to easily search for and launch applications or to quickly search for file and directories. The "*" wildcard
can be used in the search terms and the search will include hidden files if the search term starts with a dot ("."). :numref:`Figure %s: Search for Applications <lumina13a>` shows a
screenshot of this utility.

.. _lumina13a:

.. figure:: images/lumina13a.png

To open an application, begin to enter its name and the box below the selected "Applications" button will display any matching application names. Select the desired application and click
the "Launch Item" button to open it.

If you click the "Files or Directories" button, the screen changes slightly, as seen in :numref:`Figure %s: Search for Files <lumina13>`.

.. _lumina13:

.. figure:: images/lumina13.png

By default, a "Files or Directories" search is limited to the user's home directory, as indicated by the "Search: ~" at the bottom of the screen. The "Smart: Off" indicates
that every subdirectory is included in the search; in other words, there are no excluded directories. To add additional search directories or to exclude subdirectories, click 
the wrench icon to see the screen shown in :numref:`Figure %s: Configuring the Search Directories <lumina14>`.

.. _lumina14:

.. figure:: images/lumina14.png

Click the blue folder icon to change the starting search directory. For example, you can select "Computer" then "/" from the "Select Search Directory" screen to search the entire
contents of the computer. You can also add directories to exclude from searches by clicking the "+" button. If you add any excludes, you can delete an exclude by highlighting it
and clicking the "-" button. By default, the "Save as Defaults" option is selected. Unselect this option if you only wish to temporarily modify your search settings.

.. index:: Xconfig
.. _Lumina Xconfig:

Lumina Xconfig
==============

The :command:`lumina-xconfig` utility is a graphical front-end to the :command:`xrandr` command line utility. It provides the ability to probe and manage any number
of attached monitors. To start this utility, right-click the desktop and select :menuselection:`Settings --> Screen Configuration`, click the "User" icon then
:menuselection:`Desktop Preferences --> Screen Configuration`, or type :command:`lumina-xconfig` from an xterm. This will open a screen similar to the one shown in
:numref:`Figure %s: Configuring Monitors <lumina15>`.

.. _lumina15:

.. figure:: images/lumina15.png

In this example, two monitors are attached to the system and each is displayed along with their current screen resolution.

.. _Contributing to Lumina:

Contributing to Lumina
**********************

Lumina is an open source project which relies on involvement from its users and supporters to assist in development, documentation, and localization. This section describes how you can
assist the Lumina Project

.. _Report a Bug:

Report a Bug
============

If you like playing around with your desktop environment and have a bit of spare time, one of the most effective ways you can assist the Lumina Project is by
reporting problems you encounter while using Lumina. Subscribing to the `PC-BSD® blog <http://blog.pcbsd.org/>`_ is a good way to keep
up-to-date on the availability of new Lumina versions.

Anyone can report a Lumina bug. Follow these tips so that you can accurately describe your findings so they can be fixed as soon as possible: 

* Lumina is part of the PC-BSD® Project and Lumina bugs are reported to the PC-BSD® bug tracker. If you haven't already, click the "Register" link at
  `bugs.pcbsd.org <https://bugs.pcbsd.org>`_ and reply to the automatic email to confirm your user account.

* Use the "Search" bar at `bugs.pcbsd.org <https://bugs.pcbsd.org>`_ to see if anyone else has reported a similar problem. If a similar bug exists which has not been resolved yet,
  you can add a comment if you have additional information to aid the developers in fixing the bug. Note that you do not need to be logged in to perform a search, but you will have
  to login using the Sign in" link in order to add a comment to an existing bug or to create a new bug report.
  
* To create a new bug report, make sure you are signed in, then go to `<https://bugs.pcbsd.org/projects/pcbsd/issues/new>`_. In the screen shown in
  :numref:`Figure %s: Creating a Bug Report <bug>`, click the "Category" drop-down menu and select "Lumina Desktop".

* Input a descriptive "Subject" that includes the error and the version of Lumina. Ideally, the subject is short (8 words or less) and contains key words about the error so that other
  users with similar issues will find the bug report when they perform a search.

* In the "Description", give a short (2-3 sentences) description of how to recreate the error. If there is an error message, include its complete text. You can also attach a screenshot
  if it can help the developer in visualizing the problem.
  
* When finished, click "Create" to save the report. It will automatically be assigned a number and you will receive an email at the email address you used to register whenever a comment
  is added to the report or its status changes.
  
.. _bug:

.. figure:: images/bug.png

.. _Become a Translator:

Become a Translator
===================

If you are interested in translating Lumina into your native language, there are two translation areas that you can choose to become involved in: 

1. Translate the graphical menus within Lumina.

2. Translate the Lumina Handbook (this document). 

This section describes each of these translation areas in more detail and how to get started as a translator.

Regardless of the type of translation you are interested in, you should first join the
`translations mailing list <http://lists.pcbsd.org/mailman/listinfo/translations>`_. When you join, send an email to introduce yourself and indicate which
language(s) and which type(s) of translations you can assist with. This will allow you to meet other volunteers as well as keep abreast of any notices or
updates that affect translators.

.. index:: translations
.. _Interface Translation:

Interface Translation
---------------------

Lumina uses `Pootle <https://en.wikipedia.org/wiki/Pootle>`_ for managing localization of the menu screens seen in Lumina.
Pootle makes it easy to find out if your native language has been fully localized for Lumina. Pootle also makes it easy for users to check and submit
translated text as it provides a web editor and commenting system. This means that translators can spend their time making and reviewing translations rather
than learning how to use a translation tool.

To see the status of a localization, open up the `Lumina translation website <http://translate.pcbsd.org/projects/lumina/>`_ in a web browser, as seen in
:numref:`Figure %s: The Lumina Pootle Translation System <translate1>`. 

.. _translate1:

.. figure:: images/translate1.png

The localizations Lumina users have requested are listed alphabetically on the left. If your language is missing and you would like to help in its
translation, send an email to the `translations mailing list <http://lists.pcbsd.org/mailman/listinfo/translations>`_ so it can be added.

The green bar in the "Progress" column indicates the percentage of Lumina menus that have been localized. If a language is not at 100%, it means that the
menus that currently are not translated will appear in English instead of in that language.

If you click on a language name, you will see each menu item that is available for translation.
The example shown in :numref:`Figure %s: Viewing a Language's Available Menus <translate2>` is for the Greek localization. In this example, the menu for "lumina-search" is almost complete,
but the translation for "lumina-config" has not been started yet.

.. _translate2: 

.. figure:: images/translate2.png

In order to edit a translation, you need to first create a Pootle login account. Once you are logged in to Pootle, navigate to the menu item that you wish to
translate. In :numref:`Figure %s: Using the Pootle Interface to Edit a Translation String <translate3>`, the translator has clicked on "lumina-config.ts" then clicked the "Continue
translation" link.

.. _translate3:

.. figure:: images/translate3.png

In this example, the first string, the phrase "Select Application" has not yet been translated. To add the translation, type the translated text into the
white text field and click the "Submit" button. To translate another text field, click on the hyperlink associated with its name, or use the "Next" and
"Previous" links to navigate between text fields. Sometimes, as seen in this example, a text field exists in another screen and already has a translation. In this case,
you can click the link for a "Similar translations" and it will be added to the field for you so that you can "Submit" it.

If you need help with a translation or using the Pootle system, you can ask for help on the translations mailing list or in the
`translations forum <https://forums.pcbsd.org/forum-40.html>`_. 

.. index:: translations
.. _Documentation Translation:

Documentation Translation
-------------------------

.. _Become a Developer:

Become a Developer
==================

Developers who want to help improve the Lumina codebase are always welcome! If you would like to participate in core development, subscribe to the
`developers mailing list <http://lists.pcbsd.org/mailman/listinfo/dev>`_. 

All of the Lumina utilities are developed in C++ using the Qt Libraries, but other Qt-based languages are used for various parts of the project as well. For example, the
`Qt Stylesheet language <http://doc.qt.io/qt-4.8/stylesheet.html>`_, which is similar to CSS, is used for theme templates and
`QML <http://doc.qt.io/qt-5/qtqml-index.html>`_, which is similar to JavaScript, may optionally be used for desktop interface plugins.

.. index:: development
.. _Getting the Source Code:

Getting the Source Code
-----------------------

The Lumina source code is available from github and :command:`git` needs to be installed in order to download the source code. When using PC-BSD®,
:command:`git` is included in the base install.

To download the source code, :command:`cd` to the directory to store the source and type::

 git clone git://github.com/pcbsd/lumina.git
 git pull

This will create a directory named :file:`lumina/` which contains the local copy of the repository. To keep the local copy in sync with the official
repository, run :command:`git pull` within the :file:`lumina` directory.

In order to compile the source, make sure that the following `list of required software <https://github.com/pcbsd/lumina/blob/master/DEPENDENCIES>`_ is installed. If you are on a PC-BSD®
system, the required software is contained in the "PC-BSD Build Toolchain" PBI which can be installed using AppCafe® or by typing :command:`pkg install pcbsd-toolchain`. You will also need
to run :command:`pkg install devel/qt5-concurrent` On other operating systems, install any missing software using the operating system's package management utility.

To compile the source, first run :command:`qmake` to generate the necessary :file:`Makefile`, then run :command:`make`. The following example is for a PC-BSD® system and the binary
paths may differ on your operating system::

 cd lumina

 /usr/local/lib/qt5/bin/qmake

 make

.. note:: If you encounter an issue trying to compile source on a non-PC-BSD® system, refer to the "How to build from source" section of the
   `README <https://github.com/pcbsd/lumina/blob/master/README.md>`_ for some additional tips.
 
If you wish to also install the compiled applications, run this command which requires superuser privileges::

 sudo make install
 
For development purposes, several Qt IDEs are available. On a PC-BSD® system they can be installed using AppCafe® and these open source applications should also be available using the
software management utility of other operating systems. `QtCreator <http://wiki.qt.io/Category:Tools::QtCreator>`_ is a full-featured IDE designed to help new Qt users get up and running
faster while boosting the productivity of experienced Qt developers. `Qt Designer <http://doc.qt.io/qt-4.8/designer-manual.html>`_ is lighter weight as it is only a :file:`.ui` file editor
and does not provide any other IDE functionality.

If you plan to submit changes so that they can be included in Lumina, fork the repository using the instructions in
`fork a repo <https://help.github.com/articles/fork-a-repo>`_. Make your changes to the fork, then submit them by issuing a
`git pull request <https://help.github.com/articles/using-pull-requests>`_. Once your changes have been reviewed, they will be committed or sent back with
suggestions.

.. index:: development
.. _Design Guidelines:

Design Guidelines
-----------------

Lumina is a community driven project that relies on the support of developers in the community to help in the design and implementation of new utilities and tools. The Project aims to
present a unified design so that programs feel familiar to users. As an example, while programs could have "File", "Main", or "System" as their first entry in a menu bar, "File" is used
as the accepted norm for the first category on the menu bar. This section describes a small list of guidelines for menu and program design in Lumina.

Any graphical program that is a full-featured utility, such as :ref:`Insight File Manager`, should have a "File" menu. However, file menus are not
necessary for small widget programs or dialogue boxes. When making a file menu, a good rule of thumb is keep it simple. Most Lumina utilities do not need
more than two or three items on the file menu.

"Configure" is our adopted standard for the category that contains settings or configuration-related settings. If additional categories are needed, check to
see what other Lumina utilities are using.

File menu icons are taken from the installed icon theme. Table 5.3a lists some commonly used icons and their default file names.


**Table 5.3a: Commonly Used File Menu Icons** 

+-----------+-----------------+--------------------+
| Function  | File Menu Icon  | File Name          |
+===========+=================+====================+
| Quit      | row 1, cell 2   | window-close.png   |
+-----------+-----------------+--------------------+
| Settings  | row 2, cell 2   | configure.png      |
+-----------+-----------------+--------------------+


Lumina utilities use these buttons as follows: 

* **Apply:** applies settings and leaves the window open.

* **Close:** closes program without applying settings.

* **OK:** closes dialogue window and saves settings.

* **Cancel:** closes dialog window without applying settings.

* **Save:** saves settings and closes window. 

Many users benefit from keyboard shortcuts and we aim to make them available in every Lumina utility. Qt makes it easy to assign keyboard shortcuts. For
instance, to configure keyboard shortcuts that browse the "File" menu, put *&File* in the text slot for the menu entry when making the application.
Whichever letter has the *&* symbol in front of it will become the hot key. You can also make a shortcut key by clicking the menu or submenu entry and
assigning a shortcut key. Be careful not to duplicate hot keys or shortcut keys. Every key in a menu and submenu should have a key assigned for ease of use
and accessibility. Tables 5.3b and 5.3c summarize the commonly used shortcut and hot keys.

**Table 5.3b: Shortcut Keys** 

+---------------+---------+
| Shortcut Key  | Action  |
+===============+=========+
| CTRL + Q      | Quit    |
+---------------+---------+
| F1            | Help    |
+---------------+---------+

**Table 5.3c: Hot Keys** 

+-----------+-----------------+
| Hot Key   | Action          |
+===========+=================+
| Alt + Q   | Quit            |
+-----------+-----------------+
| Alt + S   | Settings        |
+-----------+-----------------+
| Alt + I   | Import          |
+-----------+-----------------+
| Alt + E   | Export          |
+-----------+-----------------+
| ALT + F   | File Menu       |
+-----------+-----------------+
| ALT + C   | Configure Menu  |
+-----------+-----------------+
| ALT + H   | Help Menu       |
+-----------+-----------------+


Developers will also find the following resources helpful: 

* `Commits Mailing List <http://lists.pcbsd.org/mailman/listinfo/commits>`_

* `Qt 5.4 Documentation <http://doc.qt.io/qt-5/index.html>`_

* `C++ Tutorials <http://www.cplusplus.com/doc/tutorial/>`_