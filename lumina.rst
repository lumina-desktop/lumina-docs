.. _Introduction to Lumina:

Introduction to Lumina
**********************

The Lumina Desktop Environment (Lumina for short) is a lightweight, XDG-compliant, BSD-licensed desktop environment that focuses specifically on streamlining
the ability to get work done while minimizing system overhead. It is specifically designed for PC-BSD® and FreeBSD, but has also been ported to many other
BSD and Linux operating systems. It is based on the Qt graphical toolkit and the Fluxbox window manager, and uses a small number of X utilities for various
tasks, such as :command:`numlockx` and :command:`xscreensaver`.

Lumina's features include: 

* Very little system overhead.

* Does not require any of desktop implementation frameworks such as DBUS, policykit, consolekit, systemd, or HALD.

* Does not come bundled with any applications such as web browsers, email clients, multimedia software, or office suites. Instead, it provides utilities for configuring the desktop
  environment.

* Uses a simple, `text-based configuration file for setting system-wide defaults <https://github.com/pcbsd/lumina/blob/master/lumina-desktop/defaults/luminaDesktop.conf>`_. This allows
  Lumina distributors to easily pre-set the Lumina defaults and interface for their distribution.

* Provides a plugin-based interface design. This allows the user to make the desktop as light or heavy as desired by choosing which plugins to have running on their desktop and panels.
  This plugin-based system is similar to Android or other modern operating systems.
  
* Single, easy-to-use :ref:`Lumina Configuration` utility controls all the different configuration options for the desktop in one location.

* Intelligent "favorites" system for creating quick shortcuts to applications, files, and directories.

* ZFS file restore functionality through the :ref:`Insight File Manager`.

* Simple access to operating system-specific functionality such as screen brightness, audio volume, and battery status.

* Multi-monitor support includes the :ref:`Lumina Xconfig` graphical utility for adding or removing monitors from the Lumina session.

* Simple system controls through the system menu for configuring audio volume, screen brightness, battery status/notifications, and workspace switching.

* Total system search capabilities through :ref:`Lumina Search`, without a daemon eating memory in the background.

* Screenshot functionality through :ref:`Lumina Screenshot` which is also tied to the “Print Screen” key by default.

.. _How to Get Lumina:

How to Get Lumina
*****************

Lumina is available as a pre-built package for numerous operating systems. The `Get Lumina <http://lumina-desktop.org/get-lumina/>`_ section of the webpage includes installation instructions for each supported system.

In addition to pre-built packages, the `Lumina source repository <https://github.com/pcbsd/lumina>`_ is available on GitHub so that developers can contribute code or create
packages for other distributions. If you plan to compile Lumina from source, refer to `DEPENDENCIES <https://github.com/pcbsd/lumina/blob/master/DEPENDENCIES>`_ and ensure all
dependent software is installed and to `README <https://github.com/pcbsd/lumina/blob/master/README.md>`_ for build instructions.

Once installed, add "Lumina-DE" as the name of the binary in your :file:`.startx`, :file:`.xinitrc`, or similar X startup file.

.. note:: No startup configuration is needed when installed on a PC-BSD® system as the PCDM login manager will automatically display Lumina in the login menu. Simply log out, select Lumina,
   and log back in.
   
The rest of this Handbook describes the Lumina Configuration utility and the various utilities which are built into Lumina. It then describes how you can contribute to the Lumina Project and
lists the changelogs for each version of Lumina.

.. _Start Menu:

Start Menu
**********
  
:numref:`Figure %s: Lumina Desktop <lumina1c>` A screenshot of Lumina on a PC-BSD® system. The user has clicked the "fireball" icon in order to open the start menu.

.. _lumina1c:

.. figure:: images/lumina1c.png
   :width: 896px
   :height: 503
   :scale: 100%
   

The start menu provides quick access for user interaction with the system. The top frame indicates which user is logged in. Hover over the battery icon to display the current status of
the battery, if your system has one, and the estimated time remaining if that battery is discharging. 

The favorites element is the largest section of the menu. Click an entry to launch that application. Right-click an entry to "Remove from Favorites" or to "Add to Quicklaunch". In Lumina, "Favorites"
appear in this section of the start menu and "QuickLaunch" adds a button for the application to the panel that is next to the start menu button.

The remainder of the start menu contains the following:

* **Browse Files:** used to browse for files and directories using the :ref:`Insight File Manager`. One of the actions available in this file manager is the ability to add a file or directory
  to the list of Favorites. Simply select the file or directory and click the star icon in Insight.

* **Browse Applications:** click this entry to browse all the applications currently registered on the system. Applications are listed alphabetically by category and the "Show Categories"
  button has three modes. Click "Show Categories" to toggle between showing just the category names (black box icon), just the contents of the categories (white box icon), or the categories
  and their contents (1/2 black 1/2 white icon). Click an application's name to start that application. If you right-click an application's name, you can "Pin to Desktop", "Add to Favorites",
  or "Add to Quicklaunch". If you are running PC-BSD® or another operating system that has a pre-defined application store, click "Manage Applications" at the top of the list of applications
  in order to open that application store. For example, on a PC-BSD® system, "Manage Applications" opens AppCafe®. Click the "Back" button to return to the start menu.

* **Control Panel:** if you are on PC-BSD®, or an operating system which provides a control panel, click this entry to open that operating system's control panel.

* **Preferences:** click this entry to access the following:


* **Configure Desktop:** click this entry to open the :ref:`Lumina Configuration` utility.

  * **Lumina Desktop Information:** click the "?" icon to determine the installed version of Lumina.

  * **System Volume:** use your mouse to move the volume control slider to change the system audio volume from 0% to 100%. Click the sound icon on the left to mute or unmute the speaker. If
    the operating system provides a mixer utility, click the speaker icon on the right to launch that mixer utility for advanced control of the audio system.

  * **Screen Brightness:** use your mouse to move the brightness control slider from 10% to 100%.

  * **Workspace:** the number of available virtual workspaces are listed. Click the right or left arrow to switch between workspaces.

  * **Locale:** this will only appear if the lumina-i18n package is installed. The current locale will be displayed as the title of the drop-down menu. Click the drop-down menu to select
    another locale for this session. Refer to :ref:`Session` for more information on fine-tuning the locale settings.

  * **Back:** click to return to the start menu.

  
* **Leave:** click this entry in order to "Suspend System" (if the operating system supports it, press the system's power button to login and resume operation) "Restart System" (if the user
  has permission), "Power Off system" (if the user has permission), "Sign Out User", or to go "Back" to the system menu. Alternately, click the "lock" icon next to "Leave" to lock the system
  and return it to a login prompt.

.. note:: On a PC-BSD system which is in the middle of applying updates, the shutdown and restart options will be disabled until the updates are complete and a note will indicate that
   updates are in progress.

.. _Panel and System Tray:

Panel and System Tray
*********************

By default, Lumina provides a panel at the bottom of the screen with a system tray at the far right of the panel. This section describes the default layout. For instructions on how to
configure the panel to suit your needs, refer to the "Panels" tab :ref:`Interface` section.
  
As you open windows or applications, a button will be added to the section of the panel near the system menu. If the application provides an icon, the button
will appear as that icon and if you mouse over it, the tooltip will show the name of the application. If you have multiple copies of an application running,
it will combine all those entries into a single button and list the number of windows after the icon. If you click on a button, it will automatically make that window active and if you
click it again, it will automatically minimize it. If there are multiple windows, you can select the particular window you want to activate from a drop-down menu.

If you right-click the title of an open window, a menu of options will appear so that you can shade, stick, maximize, iconify, raise, lower, set the window
title, send the window to a workspace, layer/dock the window, set the window's transparency, remember a specified setting, or close the window.

The system tray is located in the right portion of the panel. Any applications that register a tray icon will appear in this area. For example, on a PC-BSD system, icons will appear for
Life Preserver, Mount Tray, and Update Manager. Click or right-click an icon to interact with that application directly. The current system time shown by the clock is in the default format
for the current locale. If you click the clock icon and then click "Time Zone", a menu will open where you can select to either "Use System Time" or click a country name in order to select a
city to change to that city's time zone.
  
.. index:: right-click menu
.. _Right-Click Menu:

Right-Click Menu
****************

If you right-click the desktop, a menu of quick shortcuts will appear and the title of the menu will indicate the name of the current workspace. This section describes the default
menu items. For instructions on how to configure the right-click panel to suit your needs, refer to the "Desktop" tab :ref:`Interface` section.

By default, the right-click menu contains the following items:

* **Terminal:** used to launch a system terminal. The default is :command:`xterm`, but this can be customized.

* **Browse Files:** launches the default, and recommended, file manager, the :ref:`Insight File Manager`.

* **Applications:** provides shortcuts to the operating system's graphical software management utility (if available), the control panel (if the operating
  system provides one), and the applications currently registered on the system, arranged by system category.

* **Preferences:** contains shortcuts to the screensaver preferences, :ref:`Lumina Configuration` utility, display configuration (:ref:`Lumina Xconfig`), the operating
  system's control panel, and for determining the version of Lumina.

* **Leave:** opens the system log out window, with options to log out of the desktop session, restart the system (if the user has permission), shutdown the system (if the user has
  permission), cancel the log out window, lock the system, or suspend the system (if the operating system supports suspend mode).

.. index:: configuration
.. _Lumina Configuration:

Lumina Configuration
********************

The Lumina Configuration utility, shown in :numref:`Figure %s: Lumina Desktop Configuration <lumina3b>`, can be used to configure every aspect of the desktop and is the recommended way to
make changes. To launch this utility, click the start menu then :menuselection:`Preferences --> Configure Desktop`, right-click the desktop and click
:menuselection:`Preferences --> Desktop`, or type :command:`lumina-config` from an xterm.
   
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
:numref:`Figure %s: Lumina Desktop Configuration <lumina3b>`, can be used to add a wallpaper ("+" button) or remove ("-" button) a wallpaper. When you click the "+" button, the drop-down
menu can be used to select the file(s), a single directory, a directory and all of its subdirectories, or a solid color to use as the wallpaper. If multiple images are selected, the "Rotate
Background" button can be selected as well as a specified time interval in minutes to rotate to the next image. 

.. _lumina3b:

.. figure:: images/lumina3b.png
   :width: 596px
   :height: 494px
   :scale: 100%
   
Click the "Layout" drop-down menu to change the default layout of "Automatic" to one of the following options: "Tile", "Center", "Top Left", "Top Right", "Bottom Left", or "Bottom Right".

.. _lumina16a:

.. figure:: images/lumina16a.png
   :width: 580px
   :height: 484px
   :scale: 100%

The options that are available when you click :menuselection:`+ --> Solid Color` are shown in :numref:`Figure %s: Modifying the Wallpaper <lumina16a>`. If you select a color and click "OK",
it will be added as a solid color background to the wallpaper selection drop-down menu.

.. _lumina17b:

.. figure:: images/lumina17b.png
   :width: 738px
   :height: 494px
   :scale: 100%
   
The "Theme" tab, shown in :numref:`Figure %s: Modifying the Theme <lumina17b>`, can be used to change the default font, font size, theme template, color scheme, icon pack, and mouse
cursors. 

.. _lumina18a:

.. figure:: images/lumina18a.png
   :width: 806px
   :height: 421px
   :scale: 100%
   
It is possible to create your own "Theme Template" or "Color Scheme" by clicking the "Edit" button next to those options and changing the settings as necessary.
:numref:`Figure %s: Using the Theme Editor <lumina18a>` shows an example of clicking the "Edit" button with the "Lumina-default (System)" theme template selected. This action opened the
"Theme Editor" and the user has clicked the color selector (dropper icon) in the upper right corner. After selecting an item in this menu, the template controlling that selection can be
edited by changing the values in the theme editor box. Note that the theme templates are written as `Qt stylesheets <http://doc.qt.io/qt-5/stylesheet.html>`_, so some scripting experience
may be helpful when configuring a theme. After making your changes, you can either click the "Save" button to save the theme without closing the editor, or click the "Apply" button which
will both save the theme and close the theme editor.



.. index:: menu, panel
.. _Interface:

Interface
=========

The "Interface" tab is used to configure the desktop right-click menu and panel. Its "Desktop" tab, shown in :numref:`Figure %s: Right-Click Menu Configuration <lumina4c>`, is used to
configure which items appear in the right-click menu and which items are embedded onto the desktop.

.. _lumina4c:

.. figure:: images/lumina4c.png
   :width: 738px
   :height: 494px
   :scale: 100%

To add an item to the right-click menu, click the "+" button under the "Quick-Access Menu". This will open the "Select a Plugin" screen where you can add an application, custom app, an entry
for the :ref:`Insight File Manager`, a separator, a shortcut to Settings, a terminal, or a listing of currently open applications. To remove an item from the right-click menu, highlight it
and click the "-" button. Use the arrow buttons to change the order of the items in the right-click menu.

To embed a utility onto the desktop, click the "+" button under the "Embedded Utilities" frame. The following plugins can be added as an icon on the desktop: Application Launcher
(opens a menu that lists which applications can be launched), Audio Player, Calendar, Desktop Icons View, Note Pad, Sample (an example of a QtQuick/QML plugin), and System Monitor (displays
CPU temperature/usage, memory usage, and disk I/O). Once you click the "Save Changes" button, any utilities you added will appear on top of the desktop. To remove an embedded utility from
the desktop, highlight its entry under "Embedded Utilities", click the "-" button, and click "Save Changes". Alternately, right-click the icon for the utility and select "Remove Item" from
the right-click menu. 

The following options are also available when you right-click an icon on the desktop, allowing you to customize the location and appearance of desktop icons: "Start Moving Item" (click the
icon to lock it in place once you have moved it to the desired location), "Start Resizing Item" (use the mouse to increase/decrease size and click when you are finished), "Increase Desktop
Icon Sizes" (increases all desktop icons, repeat as necessary), and "Decrease Desktop Icon Sizes" (decreases all desktop icons, repeat as necessary).

The "Display Desktop Folder Contents" option is used to display each item stored in :file:`~/Desktop` as an icon on the desktop. By default, this option is selected as its box is black. If
you de-select this option and click "Save Changes", the icons for the contents of :file:`~/Desktop` will be removed from the desktop.
   
To configure the panel, click the "Panels" tab which will open the screen shown in :numref:`Figure %s: Panels Tab <lumina5d>`.

.. _lumina5d:

.. figure:: images/lumina5d.png
   :width: 738px
   :height: 494px
   :scale: 100%

This screen can be used to customize the location, alignment, size, theme, and plugins for an existing panel. The "+" and "-" icons towards the top, next to "Panel 1" can be used to add
or remove additional panels. Panels must be aligned along a screen edge, opposite screen edges in the case of two panels, and may have any width, color, or transparency. 

.. note:: If you add additional panels, a frame, similar to "Panel 1", will be created for each panel, and will be labeled "Panel 2", "Panel 3", and so on. This allows you to configure
   each panel separately. The configuration tabs available for a panel are described below. Be sure to select the tab in the panel that you wish to customize.

The "Location" tab (4 arrow icon) contains the following items:

* **Edge:** this drop-down menu can be used to set the location of the panel which can be "Top", "Bottom", "Left", or "Right". 

* **Alignment:** this drop-down menu can be used to center the panel on the edge or pin it to one of the corners. 

* **Size:** can be used to specify the panel width in pixels and the panel length. 

The "Appearance" tab (monitor icon) is shown in :numref:`Figure %s: Panels Appearance Tab <lumina19b>`.

.. _lumina19b:

.. figure:: images/lumina19b.png
   :width: 738px
   :height: 494px
   :scale: 100%

If you would like the panel to be hidden unless the mouse is hovered over it, check the "Auto-hide Panel" box. The "Custom Color" option can be used to fine-tune the
panel color. Click its box, then the paint icon to select the panel color.

The "Plugins" tab (puzzle icon) is shown in :numref:`Figure %s: Panels Plugins Tab <lumina20b>`.

.. _lumina20b:

.. figure:: images/lumina20b.png
   :width: 738px
   :height: 494px
   :scale: 100%

To add a plugin as an icon to the panel, click the "+" button below the listed plugins and select a plugin from the list that appears. The available plugins include:

* **Application Launcher:** when you select this plugin, it will prompt you to select the application to launch. This will add a shortcut for launching the selected application
  to the panel.
  
* **Application Menu:** adds an application menu that contains a shortcut to your home directory, a shortcut to the operating system's graphical software management utility (if there is one),
  a shortcut to the operating system's Control Panel (if it provides one), and a list of installed software sorted by categories.

* **Battery Monitor:** hover over this icon to view the current charge status of the battery. When the charge reaches 15% or below, the low battery icon will flash intermittently
  and will change to a low battery icon when there is less than 5% charge left.

* **Desktop Bar:** adds a "star" button for automatically displaying entries for anything in the :file:`~/Desktop` folder and alternately launching the selected entry.

* **Line:** adds a separator line to the panel.

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

To remove a plugin, highlight it and click the "-" button below the listed plugins. The arrow buttons can be used to move the location of the plugin on the panel. The top of an ordered list
corresponds to either the top of a vertical panel or the left side of a horizontal panel. 

.. index:: application startup
.. _Applications:

Applications
============

The "Applications" tab, shown in :numref:`Figure %s: Lumina Applications Configuration <lumina6b>`, is used to configure which applications start when you login to Lumina as well as the
default applications and file types.

.. _lumina6b:

.. figure:: images/lumina6b.png
   :width: 738px
   :height: 494px
   :scale: 100%
   
To prevent an application from starting automatically, uncheck its box.

To add an application to the auto-start configuration , click "Application" to select the application's name from a drop-down menu or click "Binary" or "File" to browse
to the location of  the application or file to open. If you select a file name, Lumina will automatically open it in an application that is capable of reading the file type.

To configure the default applications and file types, click the "File Defaults" tab. In the screen shown in :numref:`Figure %s: Lumina Defaults Configuration <lumina7c>`, you can configure
the default web browser, email client, file manager, and virtual terminal. 

.. _lumina7c:

.. figure:: images/lumina7c.png
   :width: 738px
   :height: 494px
   :scale: 100%
   
Click the gear icon or the name of the existing application to select the desired application from a menu of available applications.
If you wish to go back to the default application, click the current application's name, then click "Restore Defaults".

This screen can also be used to set the default application for several categories of file types. To add an application, select the file type and either
click "Set App", which will open a drop-down menu of common applications, or "Set Binary", which will open a file browser so that you can browse to the path
of the application.
  
.. note:: Some applications, such as web browsers, keep their own internal lists of default applications for opening particular types of files. If you set
   that application to use the :command:`lumina-open` or :command:`xdg-open` utilities, it will use the default applications that are set here so that
   there is only a single list of default applications for the system.

.. index:: shortcuts
.. _Shortcuts:

Shortcuts
=========
  
The "Shortcuts" tab, shown in :numref:`Figure %s: Lumina Shortcuts Configuration <lumina8a>`, is used to configure various keyboard shortcuts for system or window tasks. Most of these
options relate to window and workspace management, such as moving windows between workspaces, but there are also options for changing the system audio volume
or screen brightness. 

.. _lumina8a:

.. figure:: images/lumina8a.png
   :width: 738px
   :height: 494px
   :scale: 100%
      
To create a shortcut, click the desired entry, then "Change Shortcut", then the key combination you wish to set. Note that any entry that already has a defined shortcut showing in the
"Keyboard Shortcut" column  can **not** be assigned to another action. First, highlight that shortcut, click "Clear Shortcut", then "Save Changes". You can now create a new shortcut.

.. index:: session
.. _Session:

Session
=======

The "Session" tab, shown in :numref:`Figure %s: Session General Options Tab <lumina12d>`, governs the general settings for the desktop session. These settings are usually not changed on a
frequent basis.

.. _lumina12d:

.. figure:: images/lumina12d.png
   :width: 738px
   :height: 494px
   :scale: 100%

The "General Options" tab can be used to automatically enable numlock, to play chimes when Lumina starts or exits, and to change the icon that appears  in the login menu and the start
menu button. It also has options to set the time format, date format, and time display format. Buttons are available to reset these options to either the system defaults or Lumina defaults.

The "Locale" tab is shown in :numref:`Figure %s: Session Locale Tab <lumina21a>`.

.. _lumina21a:

.. figure:: images/lumina21a.png
   :width: 738px
   :height: 494px
   :scale: 100%

The lumina-i18n package provides localization files. Once installed, this allows you to customize which locale is used for the various items listed in
:numref:`Figure %s: Session Locale Tab <lumina21a>`. To install this package on a PC-BSD or FreeBSD system, use :command:`sudo pkg install lumina-i18n`. On other operating systems, use the
software management tool that comes with the operating system. If the Lumina Configuration utility was open before the installation, restart it so that the list of localizations can be
loaded into the drop-down menus of this screen. Since each setting has its own drop-down menu, you have the flexibility to select different locales for each item shown in this screen. Note
that if you make any changes in the "Locale" tab, click the "Save Changes" button and restart Lumina so that the configured locales can be loaded.

Installing the lumina-i18n package will also add a drop-down menu to the "Preferences" of the start menu, though you will need to restart Lumina after the package installation in order
for the locale menu to appear in "Preferences". This drop-down menu can be used to temporarily change the locale for this session only. This will immediately change the
localization of any translated menu items on the fly so that you do not have to log back into the Lumina session.

.. note:: Any menu items that continue to be displayed in English have not been translated to the selected language yet. You can assist the Lumina Project in translating menu items using the
   instructions in :ref:`Interface Translation`.

The "Window System" tab, shown in :numref:`Figure %s: Session Window System Tab <lumina22a>`, contains various configuration options for the window manager. 

.. _lumina22a:

.. figure:: images/lumina22a.png
   :width: 738px
   :height: 494px
   :scale: 100%
   
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
   
This utility can be used to take screenshots of the desktop or selected window and save them as PNG image files. To launch this utility, click the start menu and select
:menuselection:`Browse Applications --> Utility --> Lumina Screenshot`, right-click the desktop and select :menuselection:`Applications --> Utility --> Lumina Screenshot`, type
:command:`lumina-screenshot` from a terminal window, or press the :kbd:`Print Screen` button.

On the "New Screenshot" tab, seen here in :numref:`Figure %s: New Screenshot Tab <lumina9a>` the following settings can be used to fine-tune the screenshot:

.. _lumina9a:

.. figure:: images/lumina9a.png
   :width: 351px
   :height: 310px
   :scale: 100%
   
* **Entire Session:** will take a screenshot of the entire screen.

* **Single Screen:** in a multi-monitor setup, you can select which screen number to use for the screenshot.

* **Single Window:** will screenshot a selected window. Simply choose "Single Window," then the "Take Screenshot" button, and click on the desired window.
  The "Include Borders" checkbox can be used to determine whether or not the screenshot of the window is surrounded by a black border.
  
* **Delay:** in seconds. This can be used to give you time to setup the screenshot.

There are three options for taking a screenshot: clicking the "Take Screenshot" button in the lower-right corner of Lumina Screenshot, pressing :kbd:`Ctrl+N`, or clicking :menuselection:`File --> Take Screenshot`. 

After capturing a screenshot, the "View/Edit", seen here in :numref:`Figure %s: View/Edit Tab <lumina9b>` tab provides additional options for manipulating the screenshot:

.. _lumina9b:

.. figure:: images/lumina9b.png
   :width: 351px
   :height: 310px
   :scale: 100%
   
* **Image Preview:** displays the captured screenshot. Right clicking the image will provide options for zooming in or out. Left click and dragging across the image will highlight an area which
  can be cropped by pressing the "Crop" button in the lower-right corner.
  
* **"Save As":** button to open a window where you can specify the filename and location for saving the screenshot.

* **Launch Editor:** button to launch a selectable image manipulation program.

Additionally, clicking :menuselection:`File --> Quick Save` will automatically save the screenshot to the default "Pictures" directory and open a window to select an image manipulation program.

.. index:: file manager
.. _Insight File Manager:

Insight File Manager
====================
  
The Insight file manager, shown in :numref:`Figure %s: Insight File Manager <lumina10>`, allows the user to easily browse and modify files on the local system on a per-directory basis. To
open Insight, click the start menu and select "Browse Files", right-click the desktop and select "Browse Files", or type :command:`lumina-fm` from an xterm.

.. _lumina10:

.. figure:: images/lumina10.png
   :width: 567px
   :height: 441px
   :scale: 100%
   
It is possible to open up additional directories through the tab system using :kbd:`Ctrl-T` or by clicking :menuselection:`File --> New Browser`, allowing the user to easily manage multiple
locations on the system. Insight also features the ability to "bookmark" locations on the system for instant access via the "star" button. Once a location has been bookmarked, it will be
available via the "Bookmarks" menu at the top of the window. Any removable devices that are available on the system will show up in the "External Devices" menu, if supported by the operating
system. When an item is selected, the icons on the left side of the screen provide the possible actions that may be taken with regards to that item. Possible actions include: "open item",
"open item" (will prompt to select the application to use), "add item to personal favorites", "rename item", "cut items (add to the clipboard)", "copy items to the clipboard", "paste items
from clipboard", and "delete items". By default, the action buttons are visible. They can be made invisible by clicking :menuselection:`View --> Show Action Buttons`. To disable thumbnails,
uncheck :menuselection:`View --> Load Thumbnails`. Note that this option does not remove thumbnails that have already been loaded, it only prevents loading thumbnails in new directories.
Hidden files are not shown by default; this can be changed by checking :menuselection:`View --> Show Hidden Files`.

If you select a file or directory and right-click it, the following options become available: "Open", "Open With" (where you select the application to use), "Rename",
"View Checksums" (shows the MD5 checksum), "Cut Selection", "Copy Selection", "Paste", "Delete Selection", "File Properties" (such as file type, size,
permissions, and creation date), or "Open Terminal here".

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

.. _lumina11a:

.. figure:: images/lumina11a.png
   :width: 396px
   :height: 303px
   :scale: 100%
   
* **Preferred:** these applications have registered their Mime type with the system and can open that type of file. Also included are any applications that
  have been used to open this type of file before as it keeps track of the last three applications used for that file type.

* **Available:** displays all the applications installed on the system, organized by category and name.

* **Custom:** lets the user manually type in the binary name or path of the application to use. It also provides a search button to let the user graphically
  search the system for the binary. Whenever text is entered, a check is performed to determine whether that is a valid binary and the icon will change
  between a green checkmark or a red X as appropriate.

.. index:: search
.. _Lumina Search:

Lumina Search
=============
  
Lumina Search provides the ability to easily search for and launch applications or to quickly search for file and directories. The "*" wildcard
can be used in the search terms and the search will include hidden files if the search term starts with a dot ("."). 

To start this utility, type :command:`lumina-search` or go to the start menu :menuselection:`Browse Applications --> Utility --> Lumina Search`.
:numref:`Figure %s: Search for Applications <lumina13a>` shows a screenshot of this utility.

.. _lumina13a:

.. figure:: images/lumina13a.png
   :width: 329px
   :height: 273px
   :scale: 100%
   
To open an application, begin to enter its name. The box below the selected "Applications" button will display any matching application names. Select the desired application and click
the "Launch Item" button to open it.

If you click the "Files or Directories" button, the screen changes slightly, as seen in :numref:`Figure %s: Search for Files <lumina13>`.

.. _lumina13:

.. figure:: images/lumina13.png
   :width: 288px
   :height: 273px
   :scale: 100%
   
By default, a "Files or Directories" search is limited to the user's home directory, as indicated by the "Search: ~" at the bottom of the screen. The "Smart: Off" indicates
that every subdirectory is included in the search; in other words, there are no excluded directories. To add additional search directories or to exclude subdirectories, click 
the wrench icon to see the screen shown in :numref:`Figure %s: Configuring the Search Directories <lumina14>`.

.. _lumina14:

.. figure:: images/lumina14.png
   :width: 350px
   :height: 263px
   :scale: 100%
   
Click the blue folder icon to change the starting search directory. For example, you can select "Computer" then "/" from the "Select Search Directory" screen to search the entire
contents of the computer. You can also add directories to exclude from searches by clicking the "+" button. If you add any excludes, you can delete an exclude by highlighting it
and clicking the "-" button. By default, the "Save as Defaults" option is selected. Unselect this option if you only wish to temporarily modify your search settings.
      
.. index:: Lumina File Information
.. _Lumina File Information:

Lumina File Information
=======================

The :command:`lumina-fileinfo` utility can be used to open a graphical window summarizing the size, permissions and ownership, creation time, and last modification time of the specified
file or directory. In the example shown in in :numref:`Figure %s: Sample File Information <file1>`, the user has typed :command:`lumina-fileinfo Downloads` from a terminal window to view the
file information of their :file:`~/Downloads` directory.

.. _file1:

.. figure:: images/file1.png
   :width: 521px
   :height: 426px
   :scale: 100%

.. index:: Lumina Information
.. _Lumina Information:

Lumina Information
=======================
  
This utility provides information about the version of Lumina, as well as the license, acknowledgements, and Project links. To launch this utility, right-click the desktop and select
:menuselection:`Preferences --> About Lumina`, click the start menu then the question mark icon in "Preferences", or type :command:`lumina-info` in a terminal window. An example is shown
in :numref:`Figure %s: About Lumina <about1a>`.

.. _about1a:

.. figure:: images/about1a.png
   :width: 502px
   :height: 540px
   :scale: 100%
   
The "General" tab contains the following information:

* **Desktop Version:** indicates the version of Lumina.

* **OS Build:** indicates the operating system that was used to build this version of Lumina.

* **Qt Version:** click the "View Information" button to display the QT version and its license.

* **Lumina Website:** click the "Open in web browser" link to open `<http://lumina-desktop.org/>`_ in the default web browser.

* **Source Repository:** click the "Open in web browser" link to open `<https://github.com/pcbsd/lumina>`_ in the default web browser.

* **Report a Bug:** click the "Open in web browser" link to open `<https://bugs.pcbsd.org/projects/pcbsd>`_ in the default web browser. Refer to :ref:`Report a Bug` for instructions on how
  to submit a bug report.
  
The "License" tab contains the license text for Lumina. Lumina is licensed under a `3-clause BSD license <http://opensource.org/licenses/BSD-3-Clause>`_.

The "Acknowledgements" tab contains the following:

* **Project Lead:** the name of the Project's lead developer. Click the name to open his profile on GitHub in the default web browser.

* **Contributors:** click the "Open in web browser" link to open `<https://github.com/pcbsd/lumina/graphs/contributors>`_.

* **Sponsors:** lists the project and corporate sponsors of the Lumina Project.

.. index:: Xconfig
.. _Lumina Xconfig:

Lumina Xconfig
==============
   
The :command:`lumina-xconfig` utility is a graphical front-end to the :command:`xrandr` command line utility. It provides the ability to probe and manage any number of attached monitors. To
start this utility, right-click the desktop and select :menuselection:`Preferences --> Display` or type :command:`lumina-xconfig` from a terminal window. This will open a screen
similar to the one shown in :numref:`Figure %s: Configuring Monitors <lumina15a>`.

.. _lumina15a:

.. figure:: images/lumina15a.png
   :width: 410px
   :height: 343px
   :scale: 100%
   
In this example, two display inputs are attached to the system and their current screen resolutions are displayed. If the display input supports multiple resolutions, they will appear in the
"Resolution" drop-down menu so that you can select a different resolution. 

If you attach another display input, the "Add Screen" tab is activated so that you can configure the new input's resolution and whether or not it should be the default input.

.. index:: textedit
.. _Lumina Text Editor:

Lumina Text Editor
==================
 
The :command:`lumina-textedit` utility, seen in :numref:`Figure %s: Lumina Text Edit <lumina23>` is a simple plaintext editor which features four primary elements: optional syntax highlighting, find/replace functionality, line numbering, and bracket highlighting.
Additionally, colors can be customized by selecting :menuselection:`View --> Customize Colors`.

.. _lumina23:

.. figure:: images/lumina23.png
   :width: 412px
   :height: 351px
   :scale: 100%

.. _Contributing to Lumina:

Contributing to Lumina
**********************

Lumina is an open source project which relies on involvement from its users and supporters to assist in development, documentation, and localization. This section describes how you can
assist the Lumina Project

.. _Report a Bug:

Report a Bug
============
  
If you like playing around with your desktop environment and have a bit of spare time, one of the most effective ways you can assist the Lumina Project is by
reporting problems you encounter while using Lumina. Subscribing to `Lumina News <http://lumina-desktop.org/news/>`_ is a good way to keep
up-to-date on the availability of new Lumina versions.

Anyone can report a Lumina bug. Follow these tips so that you can accurately describe your findings so they can be fixed as soon as possible: 

* Lumina is part of the PC-BSD® Project and Lumina bugs are reported to the PC-BSD® bug tracker. If you haven't already, click the "Register" link at
  `bugs.pcbsd.org <https://bugs.pcbsd.org>`_ and reply to the automatic email to confirm your user account.

* Use the "Search" bar at `bugs.pcbsd.org <https://bugs.pcbsd.org>`_ to see if anyone else has reported a similar problem. If a similar bug exists which has not been resolved yet,
  you can add a comment if you have additional information to aid the developers in fixing the bug. Note that you do not need to be logged in to perform a search, but you will have
  to login using the "Sign in" link in order to add a comment to an existing bug or to create a new bug report.
  
* To create a new bug report, make sure you are signed in, then go to `<https://bugs.pcbsd.org/projects/pcbsd/issues/new>`_. In the screen shown in
  :numref:`Figure %s: Creating a Bug Report <bug>`, click the "Category" drop-down menu and select "Lumina Desktop".

.. _bug:

.. figure:: images/bug.png
   :width: 981px
   :height: 458px
   :scale: 100%
  
* Input a descriptive "Subject" that includes the error and the version of Lumina. Ideally, the subject is short (8 words or less) and contains key words about the error so that other
  users with similar issues will find the bug report when they perform a search.

* In the "Description", give a short (2-3 sentences) description of how to recreate the error. If there is an error message, include its complete text. You can also attach a screenshot
  if it can help the developer in visualizing the problem.
  
* When finished, click "Create" to save the report. It will automatically be assigned a number and you will receive an email at the email address you used to register whenever a comment
  is added to the report or its status changes.
  
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
   :width: 800px
   :height: 453px
   :scale: 100%

The localizations Lumina users have requested are listed alphabetically on the left. If your language is missing and you would like to help in its
translation, send an email to the `translations mailing list <http://lists.pcbsd.org/mailman/listinfo/translations>`_ so it can be added.

The green bar in the "Progress" column indicates the percentage of Lumina menus that have been localized. If a language is not at 100%, it means that the
menus that currently are not translated will appear in English instead of in that language.

If you click on a language name, you will see each menu item that is available for translation.
The example shown in :numref:`Figure %s: Viewing a Language's Available Menus <translate2>` is for the Greek localization. In this example, the menu for "lumina-search" is almost complete,
but the translation for "lumina-config" has not been started yet.

.. _translate2: 

.. figure:: images/translate2.png
   :width: 800px
   :height: 453px
   :scale: 100%

In order to edit a translation, you need to first create a Pootle login account. Once you are logged in to Pootle, navigate to the menu item that you wish to
translate. In :numref:`Figure %s: Using the Pootle Interface to Edit a Translation String <translate3>`, the translator has clicked on "lumina-config.ts" then clicked the "Continue
translation" link.

.. _translate3:

.. figure:: images/translate3.png
   :width: 800px
   :height: 453px
   :scale: 100%

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

At this time, the Lumina Handbook has not yet been added to the translation system. Once it has, instructions for translating the Handbook will be added here.

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
as the accepted norm for the first category on the menu bar. 

The `Developer Guidelines <https://github.com/pcbsd/lumina/blob/5beb2730a9e8230d2377ea89e9728504ea88de9c/DeveloperGuidelines.txt>`_ contain some coding practices for getting
started with submitting updates or utilities. This section describes a small list of guidelines for menu and program design in Lumina.

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