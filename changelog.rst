.. _Changelog:

Changelog
*********

This section describes the major features and changes to each version of
Lumina, with the most recent version of Lumina listed first.

.. index:: changelog
.. _Lumina 1.2.0:

Lumina 1.2.0
============

**Major Changes**

* Dismantle the Lumina library (:file:`libLuminaUtils.so`). This is no
  longer needed or installed.
* Disable the internal Lumina Theme engine from all utilities. Now it
  is used only by the desktop while all applications use the global
  Qt5 theme engine.
* New Panel Plugins:

  * *audioplayer* (panel version of the desktop plugin with the same
    name): Allows the user to load and play audio files directly through
    the desktop itself.
  * *jsonmenu* (panel version of the menu plugin with the same name):
    Allows use of an external utility or script to generate a menu or
    contents on demand.

* New Menu Plugin *lockdesktop*: Menu option for instantly locking the
  desktop session.

* New :command:`lumina-archiver` utility: A pure Qt5 front-end to the
  *tar* utility for managing and creating archives. *Archiver* can also
  use the *dd* utility to burn an :file:`*.img` file to a USB device
  for booting.

**Updates**

* :command:`lumina-calculator`:

  * Clean up precision of reported results and how they are re-used for
    later calculations.
  * Added ability to clear or save history.
  * Tag each result with "#X" and allow that shortcut to be used in an
    equation to recall the result of that calculation.
  * Add tons of scientific functionality to the calculator without
    bloating the interface.

* :command:`lumina-config`:

  * Clean up the main page considerably: 2 columns, auto-expanded items,
    and more.
  * In the main page, add the ability to change the current Qt5 theme
    engine for external applications.
  * Add entries for newer desktop backend systems (compositor start/skip
    detection, new plugins, etc)
  * Add a new page for managing Xorg input device properties
    (requires *xinput*).
  * Add pre-defined *profiles* to the interface/panels page. Available
    options: *No panels*, *Windows*, *GNOME2/MATE*, *XFCE*, and
    *Mac OSX*
  * Add the ability to *import* panel configuration settings from one
    monitor to another, even if the original monitor is not currently
    enabled or active.

* :command:`lumina-desktop`:

  * Fix up some wallpaper update issues with monitor resizes and Fluxbox
    eccentricity.
  * Add right-click passthrough to many desktop plugins so the overall
    *plugin* menu functions no matter where the click happens on the
    plugin.
  * Fix up the panel *autohide* functionality to it will work on screen
    edges *between* monitors as well.
  * Speed up the initial start of the desktop, but delay the
    auto-started applications by 1/2 second.
  * Clean up some mimetype detection routines.
  * Clean up some more systems to ensure they use the monitor ID for
    loading or saving desktop settings.
  * Add a green background to the battery notifiers if the battery is
    fully charged, but still plugged in.
  * Make the *start menu* open faster by only re-loading the favorites
    when they change.
  * Make the *applauncher* panel plugin able to auto-complete the path
    to :file:`*.desktop` files.
  * Make the *clock* panel plugin auto-adjust the number of lines of
    text to show depending on the panel size/orientation.
  * Adjust the margins in the menus to work better on 4K monitors.
  * Clean up some vertical-panel plugin behavior.
  * Clean up the boot splash when starting the desktop. Now it displays
    the version of the desktop and some random *message of the day*, in
    addition to the normal loading indicators.

.. note:: The *message of the day* (motd) can be changed by creating a
   :file:`lumina-motd` file and placing it into :file:`<LOCALBASE>/etc`
   alongside :file:`luminaDesktop.conf`. If the new file is executable,
   Lumina will run the file and print any text that is output.
   Otherwise, it reads and displays the file contents as plaintext. For
   example, a blank file disables the motd.

* :command:`lumina-fm`:

  * Fix up some issues with directory modifications through the right
    column of a split view.
  * Fix up the re-loading of the *show hidden files* option when
    starting new viewers.
  * Re-enable drag and drop functionality (missed that with the latest
    overhaul to the viewers).
  * Fix an issue with symlinks in the path preventing the ZFS snapshot
    finder from working properly.

* :command:`lumina-open`: Update the crash monitor to only trigger when
  the process actually crashes by disabling the return code checking
  (some apps intentionally return non-zero and were getting flagged as
  crashes).

* :command:`lumina-screenshot`:

  * Add better error reporting when a screenshot can not save for some
    reason.
  * Cleanup the scaling rules for the *zoom* functionality.

* :command:`lumina-search`:

  * Apply more limits to the background search process handling.
  * Avoid trawling through the :file:`proc` directory heirarchy at all
    costs.
  * Bump the time to start the live search from 1/3 to 1/2 second.

* :command:`start-lumina-desktop`:

  * Modify the Qt5/dbus crash workaround to avoid starting up a dbus
    session if at all possible.
  * Checked and cleaned up any :command:`lumina-desktop` lockfiles.

* FreeBSD: Add PulseAudio support for TrueOS PICO sessions.

.. index:: changelog
.. _Lumina 1.1.0:

Lumina 1.1.0
============

**Major Changes:**

* :file:`trueos/lumina-i18n` repository is now depreciated. To include
  the localization files, use the :command:`WITH_I18N` build flag when
  compiling |lumina| or any of it's utilities.

* The :command:`start-lumina-desktop` utility has been significantly
  updated. It can now be used as a single command start routine for the
  |lumina| desktop. This will now automatically detect and/or start any
  background services as needed. One example is an X session or a DBUS
  session (a DBUS session is required to bypass a known bug in Qt). If
  **compton** is available and enabled for use, this binary will
  automatically set **compton** to the proper hardware/software backend
  rendering mode. By default, **compton** use will be disabled if GPU
  acceleration is not available, but this logic may be tuned as desired
  within the configuration utility.

* Significantly update how the system application list is probed and
  maintained. This results in a much lighter and faster system.

* Add the ability for |lumina| to automatically manage symlinks for
  applications within the current user's :file:`Desktop` (tunable: may
  be turned off within the user settings in the configuration utility)

* Add a new OS integration: System update detection at logout time with
  a prompt for performing or skipping updates.

* Overhaul the Insight File Manager (:command:`lumina-fm`):

  * Add a menu for GIT operations (if the **git** binary is found on the
    system). Currently supported operations: **clone** a repo from
    GitHub onto the local system (graphical wizard) and **view** the
    current status of a git repo.
  * Created a completely new directory probing backend. This backend is
    designed around multi-threading, resulting in speeds which are
    orders of magnitude faster than the previous solution.

  * Created a completely new directory viewing frontend:

    * The tab and column possibilities are now integrated within each
      other, with no more distinct **modes** to toggle. Instead, tabs
      are now **always** available, and can be created or destroyed on
      demand, but within each tab there are new buttons for using single
      or dual directory columns.
    * The thumbnails option has been removed, as the new backend makes
      loading and using thumbnails for image files a trivial matter now.
    * The interface has been simplified, more options for interacting
      with a directory and/or files through the use of a smart menu
      system have been added.

  * There is a completely new file operations tray notification system:

    * All file operations are now performed in the background. A system
      tray icon shows the status of any operations, when needed.
    * This allows for multiple sets of file operations to be performed
      simultaneously without stopping usage of the file manager itself.

* Update :command:`lumina-textedit`:

  * Cleanup the find and replace options a little, making them easier to
    close with a mouse. The options also take up less space.
  * Update syntax highlighting rules and routines quite a bit.
  * Add a font selection option, so monospaced fonts can be used for
    particular types of files and formats.
  * Add detection of unsaved changes on close and prompt to save or
    discard those changes.
  * Add new syntax highlighting rules for shell scripts/files
    (:file:`*.sh`).

* Update the desktop settings to be based on monitor ID's instead of
  monitor numbers (automatic backend settings conversion when starting
  the new version). This ensures each monitor always loads the right
  settings, even if **X** decides to randomly scramble the order of the
  monitors between sessions.

* New Desktop Utility: :command:`lumina-calculator`:

  * This is a simple calculator written in Qt5.
  * Supports simple push-button operations in addition to the option to
    write and evaluate more complicated mathematical equations.
  * Displays a history of calculations and results.

**Bug fixes and other small tweaks:**

* :command:`lumina-open` will now handle binary names as inputs.

* Fixed up terminal launching abilities:

  * Auto-use default terminal for Alt-F1 shortcut.
  * Better support for binary names in addition to :file:`.desktop`
    entries.

* :command:`lumina-open` will now detect/handle directory paths better.

* Add a special check/fix for setting a cursor theme called "default"
  (only seems to impact a few various Linux distros).

* Cleanup the application of syntax highlighting rules in
  :command:`lumina-textedit`. Ensures better priority of highlighting
  rules.

* Find and fix some stability issues with :command:`lumina-fileinfo`.

* Adjust the FreeBSD CPU temperature detection a bit, so raw CPU stats
  are preferred over ACPI data.

* Bundle in a single fallback mimetype database file so mimetypes are
  always available within |lumina|, even if the official mimetype
  database is not found.

* Have the |lumina| utilities (**text editor**, **file manager**, etc)
  check or set the :command:`XDG_*` environment variables at start, as
  needed. |lumina| utilities will now be able to detect and use the
  proper settings and files for the current user when launching through
  utilities (such as **sudo** or **doas**) which strip the environment.

* Have the desktop wallpaper randomized *every* time a change is
  requested, rather than just the first time.

* Add support for per-workspace wallpapers (not exposed in the config UI
  yet).

* :command:`lumina-fileinfo` now shows the size of an image file, in
  addition to the thumbnail.

* Make :command:`lumina-screenshot` single instanced for keyboard
  shortcut launching and setup the application registration to always
  open a new instance as needed.

* Add a right-click option to *launch* a desktop item.

* Reduce the number of widgets or items used when generating a
  "desktop" for a monitor. This greatly increases performance of the
  system, particularly when running through a remote X/VNC connection.

* Add an audio warning to the battery monitor plugin when the system
  drops to 5% left, as well as some more *warning* styling for the
  monitor.

.. index:: changelog
.. _Lumina 1.0.0:

Lumina 1.0.0
============

* Files moved/renamed:

    * "Lumina-DE" binary is now "lumina-desktop". Full pathway change:
      /usr/local/share/Lumina-DE/* -> /usr/local/share/lumina-desktop/*
    * Moved the "runtime" directory in the user's home directory to
      :file:`XDG_CONFIG_HOME/lumina-desktop`
      (replaced :file:`~/.lumina`).
    * Changed the install directory where Lumina puts all it's files at
      install time (:file:`L_SHAREDIR/lumina-desktop/` instead of
      :file:`L_SHAREDIR/Lumina-DE/`). The required LuminaOS templates
      have been adjusted to mirror the change.
    * Localization files are now installed via the main source tree,
      which accounts for the change to :file:`SHARE/lumina-desktop`
      rather than :file:`SHARE/Lumina-DE`. Also fixed the wallpaper
      directory detection routine within :command:`lumina-config` (same
      issue - install dir change broke the path detection).

* Due to the file movement/renaming, all custom settings from previous
  versions of Lumina will be wiped. All settings will revert to the
  current 1.0.0 defaults.

* :file:`luminaDesktop.conf` changes:

    * Quicklaunch apps can now be specified within
      :file:`luminaDesktop.conf`
      in a similar manner to the "favorites" options.
    * Convert the :file:`luminaDesktop.conf` parser to allow relative
      paths/filenames for favorite or default applications.
    * :file:`luminaDesktop.conf` has been altered to include
      a number of first-install applications.
    * The :file:`luminaDesktop.conf` parser will now properly set
      mimetypes as needed.
    * Add support for running generic user generated scripts or tools
      after parsing :file:`luminaDesktop.conf`.
    * Add the ability to specify mimetype defaults within
      :file:`luminaDesktop.conf` and also allow regex wildcard matching
      when looking for default applications (ex. :file:`text/*` will
      grab all text mimetypes).
    * External scripts can be used to set up a new user after Lumina is
      initialized.
    * Allow relative paths within :file:`luminaDesktop.conf` and updated
      the default apps inside :file:`luminaDesktop.conf`.

* :command:`lumina-config` reworked:

    * Added search capabilities.
    * Rebuilt for faster startup.
    * Added advanced menus to :command:`fluxbox` and :command:`compton`
      for finer control.
    * General cleanup and fluxbox.
    * Reworked multi-screen selection functionality.
    * Ensure that :command:`lumina-config` defaults to looking in the
      system installed scripts directory for menu scripts.
    * :command:`lumina-config` can now handle non-integer values for the
      panel settings as needed.

* The Lumina Desktop binary has been reduced in size.

* New application registrations:

    * lumina-fileinfo.desktop
    * lumina-config.desktop

* New optional dependencies:

    * Compton (recommended compositing manager)
    * xcompmgr (fallback manager)

* Compositing can now be disabled entirely by manually editing
  :file:`/usr/home/tmoore/.config/lumina-desktop/sessionsettings.conf`
  and adding the line :command:`enableCompositing=false`.

* New external script support:

    * Added a new type of menu plugin: "jsonmenu". This is a recursive,
      auto-generating menu which runs an external utility (a script of
      some kind usually), which generates a JSON document/object which
      is used to populate the menu.
    * User created scripts.

* Add the new JSON menu generation scripts to the "core" files installed
  as they are listed as another plugin option.

* Add options for grouped windows in the task manager: "Show All",
  "Minimize All", and "Close All".

* :command:`lumina-fileinfo` can now be used to create new application
  registrations. By default, applications are registered for the
  current user on the system, unless otherwise specified. It can
  also install it's own :file:`.desktop` registrations on the system
  during installation.

* Fixed a bug where panels display with only 5 pixels.

* Fixed a crash with the user button logging out the user.

* Fixed the xterm window title displaying nonsense.

* Fixed :command:`fluxbox` config files.

* Added the "Advanced/Simple" editors to the :command:`fluxbox` keys
  page.

* The process of finding icons has been reworked for better
  functionality.

* New wallpaper sizing options: "Fit" and "Full".

* Released a new desktop plugin: "rssreader". This plugin displays an
  active RSS feed in a configurable window set to the lower right corner
  of the screen by default. This plugin supports the RSS v0.91 and v2.0
  standards.

* Reset which directories are monitored for apps to be installed into
  every time the watcher updates (this fixes the detection of KDE apps
  being installed/removed).

* Improved backend search routine for finding :file:`.desktop` files or
  binaries.

* The calendar plugin will now move to next day if the system remains on
  over 24 hours.

* :command:`lumina-fm` will remove broken symlinks when deleting
  directories.

* Load previous screen config on Lumina start.

* Fixed the detection and usage of the "mailto:" option in
  :command:`lumina-open`. This also changes the default mimetype used
  for email applications to "application/email".

* The start menu now hides duplicate "favorite" entries.

* Added a search bar to the start menu to provide users an efficient
  method to search for apps or utilities directly.

* User button - now displays only one entry for applications linked via
  both the desktop and favorites category.

* The nongrouping task manager now uses a uniform size for panel
  buttons.

* Pressing the :kbd:`Windows button` will open the Start Menu/User
  Button/ Application Menu, whichever is the default system button.

* Build systems updates:

    * Localizations have been moved from `NO_I18N` to `WITH_I18N`. This
      will ensure that the source version of the localizations are not
      installed unless explicitly requested (since the "real"
      localization files are in the lumina-i18n repo - these source
      files are the autogenerated ones before getting sent up to the
      pootle localization system).
    * Users can add custom :file:`luminaDesktop.conf` files for a
      particular operating system to simplify builds. Customized
      :file:`luminaDesktop.conf` files can also pull in default
      wallpapers for the system.
    * To bypass OS settings check - use "DEFAULT_SETTINGS=<some OS>" in
      :file:`luminaDesktop.conf`.

* A new theme titled "Glass" has been added.

* Added :kbd:`Control+[shift]+Tab` shortcuts for cycling between open
  windows in grouped order rather than open order
  (:kbd:`alt+[shift]+tab` does open order).

* Non-applauncher desktop plugins now fill in from the bottom-right of
  the screen. This provides easily visible separation between the
  auto-generated launchers and other plugins.

* Have the :command:`lumina-open` dialog show applications on the main
  list which also have the hidden flag set (since this is for using the
  app to launch something else - these apps are now valid to show).

* Lumina Text Edit has a new symlink :command:`lte` for quick launching
  the editor from the command line.

* Fixed the symlink creation routine in :command:`lumina-textedit` to
  work with package systems.

* Set up a recursive :command:`xinit` call within the
  :command:`start-lumina-desktop` binary as needed. This call detects if
  an "X" session is already active, and starts "X" if inactive.

* Added the ability for custom, system-wide environment variable
  settings within :file:`/usr/local/etc/lumina-environment.conf` This
  allows a system admin the ability to setup customized build
  environment settings on a global basis. User settings are treated as
  overrides for the system settings.

* Disabled autoraise in :command:`fluxbox` by default.

* Fixed a crash when right-clicking a non-applauncher desktop plugin and
  removing it.

* Fixed a crash within the userbutton plugin which would happen after
  clearing out one of the scroll areas.

* Fixed the resizeMenu's mouse event handling to ensure it keeps
  control of the mouse during resize events.

* Add a new :file:`LuminaUtils` function for converting a .desktop or
  binary name into a full path (searching all the various system
  directories until it finds the file).

* The quick command run routine will now never hang the system for more
  than 1 second of inactivity from the subprocess.

* Allow the "save file as" option within lumina-textedit to always be
  available and not dependent on changes to the file.

.. index:: changelog
.. _Lumina 0.9.0:

Lumina 0.9.0
============

* Created a "Common Applications" tab in the
  :menuselection:`Lumina Configuration Utility --> "Applications"`
  section and moved common applications settings from the
  "File Defaults" tab.

* Changed the default wallpapers for Lumina/PC-BSD and added some more
  4K Lumina wallpapers.

* Updated :command:`lumina-screenshot`: Added a new quicksave option and
  launch editor button for opening a full editor, windows to be snapshot
  may now be clicked on for selection rather than using the list of open
  windows, and screenshots may be cropped as needed within the utility
  before saving them to a file.

* Added new Utility: :command:`lumina-textedit`. This is a simple
  plaintext editor with syntax highlighting, find/replace support, line
  numbers, and bracket highlighting.

* Updated the Lumina theme engine to no longer use stylesheets to modify
  non-desktop applications (including the Lumina tools/utilities). This
  opens the door for a full Qt5 theme plugin to be used for non-desktop
  utilities instead.

* Updated which XDG mime-types are used for the default web browser and
  file manager. This should make it align a bit better with what
  applications expect (if they try to read/use the database directly -
  such as some popular web browsers do).

* Updated Linux harddrive device detection ("nvme" devices).

* Added Gentoo Linux support and an "ebuild" file.

* Cleanup of some minor source syntax issues with Qt 5.6

* Fixed a number of multi-monitor issues. Screen resizes/changes will
  now be properly detected on the fly (on any system - including VM's),
  and panels will be placed properly on monitors not aligned with the
  y=0 axis.

* Ensured the current system volume gets saved on logout so it can be
  reloaded on next login (in case the volume was changed by some
  external tool during the session).

* Added new startup binary: :command:`start-lumina-desktop`. This will
  be used as the primary "entry point" for launching the desktop as
  opposed to the "Lumina-DE" binary (please adjust your .xinitrc files
  and wrapper scripts as needed). The xsession desktop entry that Lumina
  installs was already changed to run this tool, so graphical desktop
  managers should be unaffected by this change. This tool will
  eventually be used to perform the X session setup/configuration
  (so CLI users will not need to run :command:`xinit` or
  :command:`startx` directly anymore), but the X integration has not
  been implemented yet.

* Updated the FreeBSD appstore shortcut to point to the new
  appcafe.desktop file from PC-BSD.

* Cleaned many old shell scripts from the source tree (not needed for
  builds any more).

* Streamlined the build procedures slightly.

* Reorganized the source tree. Now all the Lumina tools/utilities are
  kept separate from the general build scripts/files within a
  :file:`src-qt5` directory, and additionally organized into categories
  (core, core-utils, desktop-utils). Automated build systems should not
  be impacted by this change, as the main project file (lumina.pro) has
  been left in the same place within the repository and just had all the
  internal paths adjusted accordingly.

* Updated all the installed desktop entries to use relative paths for
  the icons (better cross-OS support).

* Fixed the detection of "sloppy" URL's given to lumina-open.

* Adjusted one of the include files for the Lumina library so external
  applications can now link against the lib without the availability of
  the Lumina source tree (although still not recommended).

* Stability fix for the desktop when an invalid desktop plugin is
  set/registered.

.. index:: changelog
.. _Lumina 0.8.8:

Lumina 0.8.8
============

* Add 3 different view modes for applications in the start menu:
  Alphabetical (no categories), Partial Categories, or Categories (need
  to click the category to go into it and see the applications).

* Make the symlink icon overlays a bit smaller at 1/3 icon size instead
  of 1/2.

* Add a new button for the audio controls to the left side of the
  :menuselection:`Start --> Preferences` menu for muting and unmuting
  audio.

* The RPM spec for Fedora/CentOS has been refactored.  Within the limits
  of supporting both Fedora and CentOS 7, 32-bit and 64-bit builds can
  be done from the same spec, so that it complies with Fedora's
  guidelines on how a package should be structured.

* Improvements to the notepad desktop plugin.

* Redo the "App Menu" panel plugin so that it uses a self-contained menu
  and lists the logout options at the bottom.

* Fix sorting of "favorites" items in the "Start" menu to be sorted by
  display name instead of file name.

* Add new options for loading new wallpaper files in
  :command:`lumina-config`: Single Directory (all images within the
  directory) and Recursive Directory (all images in the selected
  directory and all sub-directories).

* Add support for selecting a ZFS snapshot by name, in addition to the
  current time-slider.

* NetBSD is now a supported build target.

* Add the ability to change monitor resolutions in
  :command:`lumina-xconfig`.

* Add support for the Intel backlight, if available, on FreeBSD systems.

* Fixed a translation bug for the Portuguese language.

* Fix a crash on FreeBSD 11.x when removing a desktop icon.

* Fix a multi-threading issue randomly causing :command:`lumina-fm` to
  crash when opening a directory.

* Fix some resize bugs with the custom resizeMenu class which is used by
  the "Start" menu.

* Multiple fixes for resolution detection as well as graphical glitches
  that were causing menus to behave unpredictably.

.. index:: changelog
.. _Lumina 0.8.7:

Lumina 0.8.7
============

* Convert everything to XCB and remove XLib dependencies.

* Update DragonFlyBSD support.

* Adjust build procedures to better support multiple concurrent threads
  using the "-j<#threads>" :command:`make` option.

* Add better relative path support for launching applications in the
  mimetype database.

* Add support for a new instance of a LuminaSingleInstance application
  using the "-new-instance" CLI flag.

* Add better fallback methodology for detecting and fixing stale
  single-instance flags.

* Now uses the Qt5-Concurrent build module for additional
  multi-threading support in various utilities.

* Add support for selecting a mouse cursor theme (requires session
  restart).

* Add new color schemes: Grey-Dark, Solarized-Light, Solarized-Dark, and
  Blue-Light.

* Customize the Lumina-default theme.

* Add inheritance to theme files and convert the Lumina-default to
  inherit the "None" theme.

* Add support to |lumina| :ref:`Screenshot` for multi-screen
  arrangements and for including and excluding window borders for single
  window snapshots.

* Add support for various background image scaling and placement
  options.

* Add a number of new desktop shortcuts for the session. This requires
  existing users to remove their :file:`~/.lumina/fluxbox-keys` before
  logging in to get the new settings.

* Clean up the panel activation and detection routines to better respond
  to mouse-over events, particularly for auto-hidden panels.

* Completely overhaul the desktop plugin container system. Now it is
  completely drag and drop based with an intelligent grid of items and
  locations. Right-click, or click and hold, an item to open a menu of
  additional plugin configuration options. Note that any previous plugin
  locations will be reset to their defaults during the update to this
  new system.

* Add support for dropping files and directories from other applications
  onto the desktop, creating a symlink to the desktop folder when
  appropriate.

* Add font outlining to all desktop items so that the text is visible
  even if the font color blends into the background image.

* ZFS snapshot browsing is now seemlessly embedded within the directory
  viewer of :ref:`Insight File Manager`.

* Add support for either tabs or columns when viewing multiple
  directories at once.

* Replace the "Icon View" mode with the ability to adjust the icon sizes
  as desired.

* Add support for running the slideshow viewer and multimedia player in
  the background as separate tabs. Add the ability to zoom in/out on a
  slideshow image as desired.

* Add full drag and drop implementation to Insight File Manager. Can
  drag files and directories to external applications that support the
  standard "text/urilist" Mimetype for drag and drop operations.

* Directory and thumbnail loading is now a couple orders of magnitude
  faster than before. The thumbnail loading routine is now a completely
  separate background thread, preventing any delays in application
  functionality while loading.

* Add support for the "back" mouse button when viewing a directory.

* Completely overhaul the :ref:`File Information` utility. Now it
  is an almost complete front-end for the Qt/Lumina file information and
  XDG entry structures.

* Add support for detecting and allowing user-local Fluxbox themes in
  addition to system-local themes.

* Decrease initial loading time of |lumina| :ref:`Configuration` by
  making it load all the background image thumbnails on demand instead
  of up-front.

* Update the :ref:`Interface` used for panel configuration so that it is
  much easier to read and use.

* Update the application selection in the fileopen dialog of
  |lumina| :ref:`Open`, making it much easier to find the proper
  application to open the specified file.

* Overhaul the "Clock" panel plugin. Now it provides a menu with a
  calendar as well as an option for the user to instantly switch the
  time zone.

* New "Start Menu" panel plugin is a Windows-esque system menu which
  incorporates the functionality of both the user button and the system
  dashboard in one place. This plugin also supports creating and
  removing desktop links for applications, as well as "quick-launch"
  buttons for adding applications to the panel.

* Update the "Workspace Switcher" panel plugin so it stays in sync with
  external changes to the current workspace.

* New "Line" panel plugin provides a simple visual line to provide
  separation between plugins.

* Fix or bypass some Fluxbox window placement bugs.

* Fix some bugs in the user button regarding file and directory
  removals.

* Clean up a number of built-in text strings for clarity and
  consistency.

* Ensure that graphical sliders for adjusting screen brightness only go
  down to 10% to prevent the user from blacking out their screen
  entirely.

* Update the support for non-xterm terminal emulators to be opened
  within a particular directory.

* Update URL syntax handling in |lumina| :ref:`Open`.

* Update support for sticky windows to appear in the task manager on all
  workspaces.

* Clean up a number of possible bugs with regards to how external
  application might be launched or used. This fixes the random race
  condition where a process finished but the thread in Lumina which
  called it still thinks it is running.

* Ensure that all calendar widgets on the desktop or panel update as
  necessary to ensure the correct date is shown during multiple-day
  sessions.

* Add a small CLI flag to |lumina| :ref:`Open` for testing the crash
  handler ("-testcrash").

* Ensure that on FreeBSD, the disk I/O information uses instantaneous
  values instead of system averages.

.. index:: changelog
.. _Lumina 0.8.6:

Lumina 0.8.6
============

* Add the ability to set system-locale overrides, used on login. This
  allows the user to mix locale settings for the various outputs.

* Add the ability to switch the locale of the current session on the
  fly, changing all locale settings for the current session only. These
  settings will be used when launching any applications within that
  session.

* Fix up the translation mechanisms so that everything is instantly
  re-translated to the new locale.

* More languages are now fully translated. Install the x11/lumina-i18n
  port or pkg to install the localizations and enable these new
  localization features.

* Add support for the “Actions” extension to the XDG Desktop
  specifications. This allows applications to set a number of various
  actions, or alternate startup routines, within their XDG desktop
  registration file. These actions are shown within Lumina as new
  sub-menus within the "Applications" menu as well as in the "User"
  button. Look for the down arrow next to the application's icon.

* Change the Lumina On-Screen-Display to a different widget, allowing it
  to be shown much faster.

* Add new *_ifexists* functionality to any session options in
  :file:`luminaDesktop.conf`. This allows the distributor to more easily
  setup default applications, such as the web browser or mail client,
  through an intelligent tree of options.

* Apply a work-around for new users which fixes a bug in Fluxbox where
  the virtual desktop windows could still be changed or closed by
  various Fluxbox keyboard shortcuts. If an existing user wants to apply
  this fix, replace their :file:`~/.lumina/fluxbox-keys` with
  :file:`/usr/local/share/Lumina-DE/fluxbox-keys`. Note that this will
  overwrite any custom keyboard shortcuts.

* Fix some bugs in the new window detection and adjustment routines with
  full-screen apps that modify the X session settings.

* Fix a couple bugs with the automatic detection and load routines for
  the new QtQuick plugins.

* Add in the :kbd:`Ctrl-X` keyboard shortcut for cutting items in the
  :ref:`Insight File Manager`.

* Fix up the active reloading of icons when the icon theme changes.

.. index:: changelog
.. _Lumina 0.8.5:

Lumina 0.8.5
============

* The user button has received a significant speed boost, and can now be
  used for browsing files and directories within the user’s home
  directory.

* Desktop icons have received a large number of changes in styling,
  amount of visible text, and functionality. There is also a new feature
  to automatically generate plugins for items in the user’s Desktop
  directory, where each plugin may be individually moved/changed rather
  than trapped within a container like the “desktopview” plugin.

* Added a desktop plugin for monitoring the system hardware status such
  as memory and CPU usage, CPU temperature, and disk I/O. This
  functionality requires operating system support and is currently only
  available for PC-BSD®, FreeBSD, and Debian.

* Added a desktop plugin container for running custom QtQuick/QML
  scripts. While there is only a single sample plugin of this type
  available at the present time, it is now possible for users to create
  their own custom interface plugins using the QML scripting language,
  which is similar to JavaScript or CSS.

* Lumina has been fully translated to German, Russian, and Spanish, and
  almost-completely translated to Catalan (89%), Chinese (61%), Estonian
  (53%), Indonesian (76%), Polish (89%), Portuguese (89%),
  Portuguese-Brazilian (89%), Swedish (91%), and Turkish (88%).

* The new system for desktop plugin settings requires that any desktop
  plugins be reset back to defaults when upgrading to this version of
  Lumina.

* There is a known conflict between Qt 5.4+ and Fluxbox 1.3.7 which
  prevents the “close” button from working on unlocked desktop plugins.
  To work around this issue, right-click on the title for the plugin and
  select the “close” option from the menu to remove the desktop plugin.
  Alternatively, you may also remove desktop plugins using the
  :ref:`Configuration` utility.

.. index:: changelog
.. _Lumina 0.8.4:

Lumina 0.8.4
============

* The panel has been improved to add support for mouse tracking,
  variable-length panels that use a percentage of the screen edge
  length, and the ability to pin the panel to a particular location on
  the screen edge by either corner or centered.

* Rescale the panel size if the monitor used in the previous session was
  a different screen resolution.

* For hidden panels, 1% of the panel size is visible on the screen while
  it is hidden, rather than using a hard-coded pixel size. This is
  better for high-resolution screens.

* Remove the restriction that panels be on opposite screen edges.

* :ref:`Lumina Search` now supports the ability to change "Files or
  Directories" search preferences on a temporary basis. New command-line
  flags can be used to start searches instantly.

* Search functionality has been integrated into the
  :ref:`Insight File Manager`. The :kbd:`Ctrl-F` keyboard shortcut or
  the “Search” menu option will start a search for a file or directory
  with the current directory as the starting point.

* A “Search” button has been added to the  home directory browser in the
  user menu. This allows the user to easily start searching for a file
  or directory within the selected directory.

* The new “Favorites” system backend is much faster and more reliable
  than the old system of symbolic links. Existing favorites should be
  automatically converted to the new format when you log into the new
  version of Lumina.

* The :command:`lumina-fileinfo` utility can be used to view basic file
  information, such as timestamps, owner/group information, file size,
  and read/write permissions. If the file is an XDG desktop shortcut
  that the user has permission to modify, this utility provides the
  ability to make changes to that shortcut by right-clicking on files in
  the desktop view plugin or within the :ref:`Insight File Manager` and
  selecting the “Properties” option.

* Better application recommendations for files and URLs, especially for
  web browsers or email clients.

* Major cleanup of XCB library usage.

* Hardware-brightness controls now used for PC-BSD® by default, if
  supported by the system hardware.

* Putting the system into the suspend state is now supported for PC-BSD®
  and Debian.

* New clock display formats.

* A large number of session cleanup and session initialization
  improvements, including resetting the user’s previous screen
  brightness and audio volume settings.

* New default keyboard shortcuts for tiling the open windows on the
  screen, on new user configurations only.

* Better support for the URL input format when required by an
  application.

* The user’s “log out” window appears much faster when activated.

* There is a known bug in Lumina 0.8.4 regarding “unlocked” desktop
  plugins. The close and maximize buttons for the plugin are
  unresponsive when using Qt 5.4.1, preventing the user from easily
  removing or maximizing a desktop plugin. As a temporary workaround,
  right-click the titlebar for the unlocked plugin and select close or
  maximize from the menu.

.. index:: changelog
.. _Lumina 0.8.3:

Lumina 0.8.3
============

* Add “Application Launcher” panel plugin which allows the user to pin
  the shortcut for an application directly to a panel.

* Add |lumina| :ref:`Xconfig`, a graphical front-end to
  :command:`xrandr`. This utility can be used to easily enable or
  disable additional monitors and screens within the current desktop
  session. Shortcuts to this utility are available in the user button
  plugin and the settings menu plugin.

* Fix the issue with transparent system tray icons on FreeBSD 11.

* Add support for the XDG autostart specifications.

* Fix a number of bugs related to detecting and using XDG mimetypes.

* Add support for the XDG autostart specifications. More work is
  necessary to convert the current Lumina autostart specification.

* Add some additional fallback routines to account for possible errors
  in :file:`*.desktop` files.

* Add support for creating new (empty) files using
  :ref:`Insight File Manager`.

* Add an option for enabling and disabling the use of image thumbnails.
  This is useful if you have massive image directories, just be sure to
  disable thumbnails **before** loading the directory.

* Add initial drag-and-drop support for moving files and directories
  within a directory.

* Load the specific icon for any application shortcuts.

* Add the ability to view file checksums.

* Add some additional checks and excludes for copy/move operations in
  the background to prevent the user from performing illegal operations,
  such as moving a directory into itself.

* Add support for listing statistics about the current directory such as
  number of files, total size of files, and percent of the filesystem
  which is used.

* Streamline the frequency of the background directory checker so that
  it runs much less often.

* Disable the shutdown/restart options on PC-BSD® if the system is in
  the middle of performing updates in order to add an extra layer of
  safety.

* Have the shutdown/restart options use the “-o” option on FreeBSD and
  PC-BSD® so that the system performs the action much faster.

* Add support for thumbnails, increasing/decreasing icon sizes, removing
  files, and  cut/copy files to the “desktopview” desktop plugin. This
  plugin provides traditional desktop icons.

* Add support for increasing and decreasing the icon size for the
  application launcher desktop plugin.

* Update the icon used for the “favorites” system in the user button and
  the file manager.

* Add the ability to display alternate timezones in the system clock.
  This does **not** change the system time as it is just a setting for
  the visual clocks/plugins.

* Add a new panel plugin for pinning application shortcuts directly to
  the panel. This is just like the “applauncher” desktop plugin, but on
  the panel.

* Perform the initial search for applications on the system within the
  session initialization. This ensure that buttons and plugins are
  responsive as soon as the desktop becomes visible.

* Fix an issue with transparent system tray icons on FreeBSD 11 and
  convert the system tray embed/unembed routines to use the XCB library
  instead of XLib.

.. index:: changelog
.. _Lumina 0.8.2:

Lumina 0.8.2
============

* Added :command:`lumina-info` which can be used to display information
  about the Lumina desktop, such as the version, license, and link to
  the source repository.

* Large overhaul of the theme templates and color schemes which are
  available out-of-box.

* The :command:`lumina-config` utility has been rearranged so that its
  UI is more intuitive and there is a new dialog for selecting plugins.
  It now has the  ability to set preferred time and date formats and the
  ability to reset default applications back to their default,
  non-mimetype registrations.

* The :ref:`Insight File Manager` has been improved. All file operations
  happen in a separate thread so that the UI does not lag any more and
  the detection of Qt-editable image files has been fixed.

* Added support to update the vertical panel display of the clock
  plugin. Various desktop plugin stability issues have been fixed and
  the  session cleanup routine has been streamlined. A second panel is
  now supported and the number of filesystem watchers has been reduced
  to one per-session instead of one per-screen.

* :ref:`Lumina Search` can now be configured to exclude directories from
  a "Files or Directories" search and to set an alternate start
  directory.

.. index:: changelog
.. _Lumina 0.8.1:

Lumina 0.8.1
============

* New "Audio Player" desktop plugin to play audio files from the
  desktop.

* New "Home Button" panel plugin to hide all windows and show the
  desktop and new "Start Menu" panel plugin which provides an
  alternative to the user button for traditional system management.

* Added the ability to remove or rotate image files while viewing a
  slideshow with :ref:`Insight File Manager`.

* New backend distribution framework for setting system-wide defaults.
  This affects new users only as existing settings will not be changed.
  Also added the ability to reset the desktop back to its defaults using
  the :ref:`Configuration` utility.

* Allow a customizable user icon which is also used in PCDM
  (PC-BSD® Display Manager).

* Panels and desktop plugins follow the current theme by default.

* The "Note Pad" desktop plugin has been converted to a file-based
  utility so that all notes can be found in :file:`~/Notes` for access
  by other utilities. Plugins are able to load a generic text file to
  treat like a note for watching or updating.

* Auto-hidden panels now stay visible when the mouse moves over the
  system tray.

* The user button opens faster now as it updates the widget on-demand in
  the background.

* Fixed a bug in |lumina| :ref:`Open` for filenames containing multiple
  "."s not detecting the file extension.

* The log-out window now opens on the current screen and the log-out
  window is hidden at the start of the log-out procedure.

.. index:: changelog
.. _Lumina 0.8.0:

Lumina 0.8.0
============

* Converted to Qt5 with XCB.

* New task manager mode which provides traditional task manager
  functionality.

* Task manager right-click action menu has many more options that are
  auto-generated based on the current window state.

* Better crash reporting through |lumina| :ref:`Open`.

* Better multimedia support using the new QMultimedia framework in Qt5.

* New custom-written single-application framework with no external
  dependencies so it works on all operating systems.

* New windows are no longer placed underneath Lumina panels, even on
  multi-monitor systems.

* Special localized characters are now recognized when passed in from
  the command line.

* Recursive file operations now function properly in
  :ref:`Insight File Manager`.

* XDG "Exec" field code replacements function better, which fixes KDE
  application shortcuts like Okular.

.. index:: changelog
.. _Lumina 0.7.2:

Lumina 0.7.2
============

* Streamlined startup process and utilities.

* Enabled login and logout chimes.

* Added the "Note Pad" and "Desktop View" desktop plugins.

* Added the :ref:`Lumina Search` utility.

* New color schemes: Green, Gold, Purple, Red, and Glass, with Glass as
  the default.

* New backend system for registering default applications using
  mime-types instead of extensions. While all Lumina utilities have been
  updated to work with the new system, previously registered defaults
  might not be transferred. You may need to reset your default web
  browser and email client using the :ref:`Configuration`
  utility.

.. index:: changelog
.. _Lumina 0.6.2:

Lumina 0.6.2
============

* A desktop plugin system has been implemented with two plugins: a
  calendar and an application launcher plugin.

* The panel plugin system has been refined with transparency support for
  the panel itself and automatic plugin resizing.

* Added the system dashboard panel plugin which allows control over the
  audio volume, screen brightness, and current workspace, while also
  displaying the current battery status, if applicable, and containing a
  button to let the user log out or shutdown/restart the system.

* The user button panel plugin has been re-implemented, incorporating
  the functionality of the desktopbar plugin. Now the user has quick
  access to files and applications in the :file:`~/Desktop` folder, as
  well as the ability to add and remove shortcuts to system applications
  in the desktop folder with one click.

* New backgrounds wallpapers and a project logo.

* Add the :ref:`Insight File Manager`. Its features include the ability
  to browse the system and bookmark favorite directories. It includes a
  simple multimedia player for playing and previewing multimedia files,
  an image slideshow viewer for previewing image files, full file and
  directory restore functionality if ZFS snapshots are available, menu
  shortcuts to quickly browse attached or mounted devices, tabbing
  support for browsing multiple directories at once, and standard file
  and directory management such as copy/paste/delete/create. Supported
  multimedia and image formats are auto-detected, so if a particular
  file is not recognized, install the appropriate library or plugin to
  provide support.

* Add |lumina| :ref:`Screenshot`, a simple utility to create and save
  screenshots. It can capture the entire system or individual windows.
  It can delay the image capture for a few seconds as necessary. This
  utility is automatically assigned to the “Print Screen” keyboard
  shortcut and is also listed in the application registry under
  "utilities".

* Add a new implementation of the :ref:`Configuration` utility.
  It can now be used to configure desktop appearance such as the
  background image and to add desktop plugins, configure the location,
  color, transparency, and size of panels as well as manage their
  plugins, with up to two panels supported per screen, configure menu
  plugins, manage global keyboard shortcuts, including shortcuts for
  adjusting audio volume or screen brightness, manage default
  applications for the system by categories or individually, manage
  session options such as enable numlock on log in or to play audio
  chimes, manage applications and files to be launched on log in, and to
  manage window system options such as appearance, mouse focus policy,
  window placement policy, and the number of workspaces.

* Update the overall appearance of the application selector window in
  |lumina| :ref:`Open`.

* Fully support registered mime-types on the system and recommend those
  applications as appropriate.
