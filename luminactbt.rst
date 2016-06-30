.. _Contributing to Lumina:

Contributing to Lumina
**********************

Lumina is an open source project which relies on involvement from its 
users and supporters to assist in development, documentation, and 
localization. This section describes how you can assist the Lumina 
Project.

.. _Report a Bug:

Report a Bug
============
  
If you like playing around with your desktop environment and have a bit 
of spare time, one of the most effective ways you can assist the Lumina 
Project is by reporting problems you encounter while using Lumina. 
Subscribing to `Lumina News <http://lumina-desktop.org/news/>`_ is a 
good way to keep up-to-date on the availability of new Lumina versions.

Anyone can report a Lumina bug. Follow these tips so that you can 
accurately describe your findings so they can be fixed as soon as 
possible: 

* Lumina is part of the PC-BSD® Project and Lumina bugs are reported to 
  the PC-BSD® bug tracker. If you haven't already, click the "Register" 
  link at `bugs.pcbsd.org <https://bugs.pcbsd.org>`_ and reply to the 
  automatic email to confirm your user account.

* Use the "Search" bar at `bugs.pcbsd.org <https://bugs.pcbsd.org>`_ to 
  see if anyone else has reported a similar problem. If a similar bug 
  exists which has not been resolved yet, you can add a comment if you 
  have additional information to aid the developers in fixing the bug. 
  Note that you do not need to be logged in to perform a search, but you
  will have to login using the "Sign in" link in order to add a comment 
  to an existing bug or to create a new bug report.
  
* To create a new bug report, make sure you are signed in, then go to 
  `<https://bugs.pcbsd.org/projects/pcbsd/issues/new>`_. In the screen 
  shown in :numref:`Figure %s: Creating a Bug Report <bug>`, click the 
  "Category" drop-down menu and select "Lumina Desktop".

.. _bug:

.. figure:: images/bug.png
   :width: 981px
   :height: 458px
   :scale: 100%
  
* Input a descriptive "Subject" that includes the error and the version 
  of Lumina. Ideally, the subject is short (8 words or less) and 
  contains key words about the error so that other users with similar 
  issues will find the bug report when they perform a search.

* In the "Description", give a short (2-3 sentences) description of how 
  to recreate the error. If there is an error message, include its 
  complete text. You can also attach a screenshot if it can help the 
  developer in visualizing the problem.
  
* When finished, click "Create" to save the report. It will 
  automatically be assigned a number and you will receive an email at 
  the email address you used to register whenever a comment is added to 
  the report or its status changes.
  
.. _Become a Translator:

Become a Translator
===================

If you are interested in translating Lumina into your native language, 
there are two translation areas that you can choose to become involved 
in: 

1. Translate the graphical menus within Lumina.

2. Translate the Lumina Handbook (this document). 

This section describes each of these translation areas in more detail 
and how to get started as a translator.

Regardless of the type of translation you are interested in, you should 
first join the `translations mailing list <http://lists.pcbsd.org/mailman/listinfo/translations>`_.
When you join, send an email to introduce yourself and indicate which
language(s) and which type(s) of translations you can assist with. This 
will allow you to meet other volunteers as well as keep abreast of any 
notices or updates that affect translators.

.. index:: translations
.. _Interface Translation:

Interface Translation
---------------------

Lumina uses `Pootle <https://en.wikipedia.org/wiki/Pootle>`_ for 
managing localization of the menu screens seen in Lumina. Pootle makes 
it easy to find out if your native language has been fully localized for
Lumina. Pootle also makes it easy for users to check and submit 
translated text as it provides a web editor and commenting system. This 
means that translators can spend their time making and reviewing 
translations rather than learning how to use a translation tool.

To see the status of a localization, open up the `Lumina translation website <http://translate.pcbsd.org/projects/lumina/>`_
in a web browser, as seen in :numref:`Figure %s: The Lumina Pootle Translation System <translate1>`. 

.. _translate1:

.. figure:: images/translate1.png
   :width: 800px
   :height: 453px
   :scale: 100%

The localizations Lumina users have requested are listed alphabetically 
on the left. If your language is missing and you would like to help in 
its translation, send an email to the `translations mailing list <http://lists.pcbsd.org/mailman/listinfo/translations>`_ 
so it can be added.

The green bar in the "Progress" column indicates the percentage of 
Lumina menus that have been localized. If a language is not at 100%, it 
means that the menus that currently are not translated will appear in 
English instead of in that language.

If you click on a language name, you will see each menu item that is 
available for translation. The example shown in :numref:`Figure %s: Viewing a Language's Available Menus <translate2>`
is for the Greek localization. In this example, the menu for 
"lumina-search" is almost complete, but the translation for 
"lumina-config" has not been started yet.

.. _translate2: 

.. figure:: images/translate2.png
   :width: 800px
   :height: 453px
   :scale: 100%

In order to edit a translation, you need to first create a Pootle login 
account. Once you are logged in to Pootle, navigate to the menu item 
that you wish to translate. In :numref:`Figure %s: Using the Pootle Interface to Edit a Translation String <translate3>`,
the translator has clicked on "lumina-config.ts" then clicked the 
"Continue translation" link.

.. _translate3:

.. figure:: images/translate3.png
   :width: 800px
   :height: 453px
   :scale: 100%

In this example, the first string, the phrase "Select Application" has 
not yet been translated. To add the translation, type the translated 
text into the white text field and click the "Submit" button. To 
translate another text field, click on the hyperlink associated with its
name, or use the "Next" and "Previous" links to navigate between text 
fields. Sometimes, as seen in this example, a text field exists in 
another screen and already has a translation. In this case, you can 
click the link for a "Similar translations" and it will be added to the 
field for you so that you can "Submit" it.

If you need help with a translation or using the Pootle system, you can 
ask for help on the translations mailing list or in the
`translations forum <https://forums.pcbsd.org/forum-40.html>`_. 

.. index:: translations
.. _Documentation Translation:

Documentation Translation
-------------------------

At this time, the Lumina Handbook has not yet been added to the 
translation system. Once it has, instructions for translating the 
Handbook will be added here.

.. _Become a Developer:

Become a Developer
==================

Developers who want to help improve the Lumina codebase are always 
welcome! If you would like to participate in core development, subscribe
to the `developers mailing list <http://lists.pcbsd.org/mailman/listinfo/dev>`_. 

All of the Lumina utilities are developed in C++ using the Qt Libraries,
but other Qt-based languages are used for various parts of the project 
as well. For example, the `Qt Stylesheet language <http://doc.qt.io/qt-4.8/stylesheet.html>`_,
which is similar to CSS, is used for theme templates and `QML <http://doc.qt.io/qt-5/qtqml-index.html>`_,
which is similar to JavaScript, may optionally be used for desktop 
interface plugins.

.. index:: development
.. _Getting the Source Code:

Getting the Source Code
-----------------------

The Lumina source code is available from github and :command:`git` needs
to be installed in order to download the source code. When using 
PC-BSD®, :command:`git` is included in the base install.

To download the source code, :command:`cd` to the directory to store the
source and type::

 git clone git://github.com/pcbsd/lumina.git
 git pull

This will create a directory named :file:`lumina/` which contains the 
local copy of the repository. To keep the local copy in sync with the 
official repository, run :command:`git pull` within the :file:`lumina` 
directory.

In order to compile the source, make sure that the following 
`list of required software <https://github.com/pcbsd/lumina/blob/master/DEPENDENCIES>`_
is installed. If you are on a PC-BSD® system, the required software is 
contained in the "PC-BSD Build Toolchain" PBI which can be installed 
using AppCafe® or by typing :command:`pkg install pcbsd-toolchain`. You 
will also need to run :command:`pkg install devel/qt5-concurrent` On 
other operating systems, install any missing software using the 
operating system's package management utility.

To compile the source, first run :command:`qmake` to generate the 
necessary :file:`Makefile`, then run :command:`make`. The following 
example is for a PC-BSD® system and the binary paths may differ on your 
operating system::

 cd lumina

 /usr/local/lib/qt5/bin/qmake

 make

.. note:: If you encounter an issue trying to compile source on a 
          non-PC-BSD® system, refer to the "How to build from source" 
          section of the `README <https://github.com/pcbsd/lumina/blob/master/README.md>`_ 
          for some additional tips.
 
If you wish to also install the compiled applications, run this command 
which requires superuser privileges::

 sudo make install
 
For development purposes, several Qt IDEs are available. On a PC-BSD® 
system they can be installed using AppCafe® and these open source 
applications should also be available using the software management 
utility of other operating systems. `QtCreator <http://wiki.qt.io/Category:Tools::QtCreator>`_
is a full-featured IDE designed to help new Qt users get up and running
faster while boosting the productivity of experienced Qt developers. 
`Qt Designer <http://doc.qt.io/qt-4.8/designer-manual.html>`_ is lighter
weight as it is only a :file:`.ui` file editor and does not provide any 
other IDE functionality.

If you plan to submit changes so that they can be included in Lumina, 
fork the repository using the instructions in 
`fork a repo <https://help.github.com/articles/fork-a-repo>`_.
Make your changes to the fork, then submit them by issuing a
`git pull request <https://help.github.com/articles/using-pull-requests>`_.
Once your changes have been reviewed, they will be committed or sent 
back with suggestions.

.. index:: development
.. _Design Guidelines:

Design Guidelines
-----------------

Lumina is a community driven project that relies on the support of 
developers in the community to help in the design and implementation of 
new utilities and tools. The Project aims to present a unified design so
that programs feel familiar to users. As an example, while programs 
could have "File", "Main", or "System" as their first entry in a menu 
bar, "File" is used as the accepted norm for the first category on the 
menu bar. 

The `Developer Guidelines <https://github.com/pcbsd/lumina/blob/5beb2730a9e8230d2377ea89e9728504ea88de9c/DeveloperGuidelines.txt>`_
contain some coding practices for getting started with submitting 
updates or utilities. This section describes a small list of guidelines 
for menu and program design in Lumina.

Any graphical program that is a full-featured utility, such as 
:ref:`Insight File Manager`, should have a "File" menu. However, file 
menus are not necessary for small widget programs or dialogue boxes. 
When making a file menu, a good rule of thumb is keep it simple. Most 
Lumina utilities do not need more than two or three items on the file 
menu.

"Configure" is our adopted standard for the category that contains 
settings or configuration-related settings. If additional categories 
are needed, check to see what other Lumina utilities are using.

File menu icons are taken from the installed icon theme. Table 5.3a 
lists some commonly used icons and their default file names.


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

Many users benefit from keyboard shortcuts and we aim to make them 
available in every Lumina utility. Qt makes it easy to assign keyboard 
shortcuts. For instance, to configure keyboard shortcuts that browse the
"File" menu, put *&File* in the text slot for the menu entry when making
the application. Whichever letter has the *&* symbol in front of it will
become the hot key. You can also make a shortcut key by clicking the 
menu or submenu entry and assigning a shortcut key. Be careful not to 
duplicate hot keys or shortcut keys. Every key in a menu and submenu 
should have a key assigned for ease of use and accessibility. 
Tables 5.3b and 5.3c summarize the commonly used shortcut and hot keys.

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