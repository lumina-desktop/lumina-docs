# lumina-docs
Lumina Handbook and Documents


The Lumina Handbook is generated from ASCII text files, that end in a .rst extension, within the pcbsd/lumina-docs source repository. Lumina uses the
Sphinx Python documentation generator to generate the documentation. Anyone can download the documentation source and generate their own copy of
the documentation in HTML or PDF formats. Users with a github account can also edit the documentation and generate git pull requests so that the edits can be
reviewed and committed. This README contains instructions for getting the source, generating a copy of the documentation, and issuing a git pull request. It
assumes that the reader is using these instructions on either a PC-BSD system or a FreeBSD jail.

##Requirements:

At a minimum, the following software needs to be installed as the root/superuser. If this is the first time you have used pkg on the system, it may prompt
you to fetch and install it. Say yes to the prompts to do so. Once it is finished, you can then finish installing the needed software.

Instructions are given for both the port and the package as some software may not have a package. Try the pkg command first as it is faster. If the pkg
command succeeds, you do not need to run the make command as the software is already installed; however if it fails, use the make command to install the
software. If the software is already installed, the pkg command will indicate that the most recent version is already installed. PC-BSD users can also
install the packages using AppCafe.

```
portsnap fetch extract
pkg install devel/git (cd /usr/ports/devel/git/ && make install)
pkg install textproc/py-sphinx (cd /usr/ports/textproc/py-sphinx/ && make install)
pkg install textproc/py-sphinxcontrib-httpdomain (cd /usr/ports/textproc/py-sphinxcontrib-httpdomain && make install)
rehash
```

If you wish to generate a PDF version of the documentation, this software also needs to be installed:

```
pkg install print/tex-formats (cd /usr/ports/print/tex-formats/ && make install)
pkg install print/tex-dvipsk (cd /usr/ports/print/tex-dvipsk/ && make install)
pkg install devel/gmake (/usr/ports/devel/gmake/ && make install)
```

Next, determine where you want to store the source code and change to that directory (we'll refer to it as /path/to/your-build-directory). Then, check out the
source code from git:

```
cd /path/to/your-build-directory
git clone git://github.com/pcbsd/lumina-docs.git
cd lumina-docs/
```

##Building the Documentation

All of the following commands need to be run from /path/to/your-build-directory/lumina-docs/. These formats are currently available: HTML, single
HTML, PDF, and EPUB. The generated output(s) can be found in /path/to/your-build-directory/lumina-docs/_build/.

To build a local copy of the HTML, with a separate page for each chapter and that chapter's table of contents in the left frame with navigational links
to browse between chapters, run the following command:

```
sphinx-build -b html . _build
```

To build a local copy of the HTML as one long page, with the entire table of contents in the left frame, use this command instead:

```
sphinx-build -b singlehtml . _build
```

To build a local PDF, run this command TWICE and ignore its error messages:

```
yes '' | gmake latexpdf
yes '' | gmake latexpdf
```

To build a local EPUB, run this command:

```
sphinx-build -b epub . _build
```

##Editing the Documentation

If you want to edit the Handbook, make changes to the lumina.rst file using any ASCII text editor.
Refer to http://docutils.sourceforge.net/docs/user/rst/quickref.html for help with formatting syntax.
Refer to http://wiki.typo3.org/Editors_%28reST%29 for a list of reST editors.

Need help getting started or want to discuss edits? Join the http://lists.pcbsd.org/mailman/listinfo/docs mailing list.

To issue a git pull request containing your edits, use the instructions at https://help.github.com/articles/using-pull-requests.

**General Table of Contents**

- [General TrueOS Information](#generalinfo)
	- [TrueOS Project Documentation](#all-docs)
		- [TrueOS Handbook](#trueos-docs)
		- [Lumina Handbook](#lumina-docs)
		- [SysAdm Handbooks](#sysadm-docs)
	- [Filing Issues or Feature Requests](#bugreporting)
	- [Community Channels](#chatchannels)
		- [Discourse](#discourseforum)
		- [Gitter](#gitterchat)
		- [IRC](#irc)
		- [Subreddit](#trueos-reddit)
	- [Social Media](#trueos-social)

<!-- END GENERAL INFO TOC -->

# General TrueOS Information

This section describes where you can find more information about TrueOS and its related projects, file new issues on GitHub, and converse with other users or contributors to the project.

## TrueOS Project Documentation

A number of [Sphinx](http://www.sphinx-doc.org/en/stable/) generated reStructuredText handbooks are available to introduce you to the TrueOS, Lumina, and SysAdm projects. These handbooks are open source, and users are always encouraged to open GitHub issues or fix any errors they find in the documentation.

### TrueOS Handbook

TrueOS documentation is hosted on the [TrueOS website](https://www.trueos.org).
The [TrueOS User Guide](https://www.trueos.org/handbook/trueos.html) is a comprehensive guide to install TrueOS, along with post-installation configuration help, recommendations for useful utilities and applications, and a help and support section containing solutions for common issues and links to community and development chat channels for uncommon issues. There is also a chapter describing the experimental TrueOS Pico project and links to the Lumina and SysAdm documentation.

### Lumina Handbook

The Lumina Desktop Environment has its own [handbook](https://lumina-desktop.org/handbook/), hosted on the [Lumina Website](https://lumina-desktop.org). This handbook contains brief installation instructions. However, due to the highly customizable nature of Lumina, the focus of the handbook lies mainly in documenting all user configurable settings. Each option is typically described in detail, with both text and screenshots. Finally, the suite of unique Qt5 utilities included with Lumina are also documented.

TrueOS users are encouraged to review the Lumina documentation, as the Lumina Desktop Environment is installed by default with TrueOS.

### SysAdm Handbooks

Due to complexity of this project, SysAdm documentation is split into three different guides:

1. **API Reference Guide** (https://api.sysadm.us/getstarted.html)

The Application Programming Interface (API) Reference Guide is a comprehensive library of all API calls and WebSocket requests for SysAdm. In addition to documenting all SysAdm subsystems and classes, the guide provides detailed examples of requests and responses, authentication, and SSL certificate management. This guide is constantly updated, ensuring it provides accurate information at all times.

2. **Client Handbook** (https://sysadm.us/handbook/client/)

The SysAdm Client handbook documents all aspects of the SysAdm client, as well as describing of the PC-BSD system utilities is replaces. Detailed descriptions of utilities such as Appcafe, Life Preserver, and the Boot Environment Manager are contained here, as well as a general guide to using these utilities. TrueOS users are encouraged to reference this guide, as the SysAdm client is included with TrueOS.

3. **Server Handbook** (https://sysadm.us/handbook/server/introduction.html)

The Server handbook is a basic installation guide, walking new users through the process of initializing SysAdm with a bridge and server connection.

## Filing Issues or Feature Requests

Due to the number of repositories under the TrueOS "umbrella", the TrueOS Project consolidates its issue trackers into a few repositories:

* [trueos-core](https://github.com/trueos/trueos-core) : Used for general TrueOS issues, Pico issues, and feature  requests.
* [lumina](https://github.com/trueos/lumina) : Issues related to using the Lumina Desktop Environment.
* (Coming Soon) [sysadm](https://github.com/trueos/sysadm) : Issues with using the SysAdm client or server.
* [trueos-docs](https://github.com/trueos/trueos-docs) : Issues related to the TrueOS Handbook.
* [lumina-docs](https://github.com/trueos/lumina-docs) : Issues related to the Lumina Handbook.
* [sysadm-docs](https://github.com/trueos/sysadm-docs) : Issues related to the SysAdm API Guide, Client, and Server Handbooks.
* [trueos-website](https://github.com/trueos/trueos-website) : Issues involving any of the TrueOS Project websites: 
  - https://www.lumina-desktop.org
  - https://www.trueos.org
  - https://www.sysadm.us

The TrueOS handbook has detailed instructions to help you report a bug (https://www.trueos.org/handbook/helpsupport.html#report-a-bug). It is recommended to refer to these instructions when creating new GitHub issues. Better bug reports usually result in faster fixes!

To request a feature, open a new issue in one of the related GitHub issue repositories and begin the title with *Feature Request:*.

## Community Channels

The TrueOS community has a wide variety of chat channels and forum options available for users to interact with not only each other, but contributors to the project and the core development team too.

### Discourse

TrueOS  has a [Discourse channel](https://discourse.trueos.org/) managed concurrently with the TrueOS Subreddit. New users need to sign up with Discourse in order to create posts, but it is possible to view posts without an account.

### Gitter

The TrueOS Project uses Gitter to provide real-time chat and collaboration with TrueOS users and developers. Gitter does not require an application to use, but does require a login using either an existing GitHub or Twitter account.

To access the TrueOS Gitter community, point a web browser to https://gitter.im/trueos.

Gitter also maintains a full archive of the chat history. This means lengthy conversations about hardware issues or workarounds are always available for reference. To access the Gitter archive, navigate to the desired TrueOS room’s archive. For example, here is the address of the TrueOS Lobby archive: https://gitter.im/trueos/Lobby/archives.

### IRC

Like many open source projects, TrueOS has an Internet Relay Chat (IRC) channel so users can chat and get help in real time. To get connected, use this information in your IRC client:

* Server name: irc.freenode.net
* Channel name: #trueos (note the # is required)

### Subreddit

The TrueOS Project also has a [Subreddit](https://www.reddit.com/r/TrueOS/) for users who prefer to use Reddit to ask questions and to search for or post how-tos. A Reddit account is not required in order to read the Subreddit, but it is necessary to create a login account to submit or comment on posts.

## Social Media

The TrueOS Project also maintains a number of social media accounts you can watch:

* Facebook: https://www.facebook.com/groups/4210443834/
* Linkedin: http://www.linkedin.com/groups?gid=1942544
* TrueOS Blog: https://www.trueos.org/blog/
* Twitter: https://twitter.com/TrueOS_Project/
