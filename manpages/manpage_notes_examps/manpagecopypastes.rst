https://forums.freebsd.org/threads/13200/

Creating a manpage from scratch.​ April 2010


What is a manpage?
The FreeBSD documentation manuals system is comprised on many manuals that
are intended to by displayed on-line from the command line using the
**man** command. Every Base RELEASE command has its own manual as well as
the commands introduced by the ports system. The layout of the manual is
standardized by the use of groff_mdoc(7) documentation macro markup
language. The files containing the source for each manual are located in
the /usr/share/man/manX/ directory tree, where the X of manX is one of
the following sections.

Code:
    Under FreeBSD 8.0, the following sections are defined:

		   1	    FreeBSD General Commands Manual
		   2	    FreeBSD System Calls Manual
		   3	    FreeBSD Library Functions Manual
		   4	    FreeBSD Kernel Interfaces Manual
		   5	    FreeBSD File Formats Manual
		   6	    FreeBSD Games Manual
		   7	    FreeBSD Miscellaneous Information Manual
		   8	    FreeBSD System Manager's Manual
                   9        FreeBSD Kernel Developer's Manual


So you would see this

Code:
               /usr/share/man/man1/
               /usr/share/man/man2/
               /usr/share/man/man3/
               /usr/share/man/man4/
               /usr/share/man/man5/
               /usr/share/man/man6/
               /usr/share/man/man7/
               /usr/share/man/man8/
               /usr/share/man/man9/



Manual File Naming Standard.
Code:
There is a standardized naming convention in place for manpage files:
       name.X.gz

Where name = the name of the command being documented.
       X   = the manual section its in from the above path list.
       gz  = means the file has been compress with gzip(1) command.

The file itself is a text file with the documentation being prefixed and 
sometimes enclosed with formatting macros from groff_mdoc(7) markup language.
Take note; The macro text file should contain no blank lines in it. 


Creating The Manual Source File.
The best way to get started is to just copy a man page from the base system 
and edit it to taste. As the system administrator I always login as user 
root so the following command examples and manual sample are developed in /root.

The manual for the jail(8) command will be used as the template for my new manual ezjail. 

Code:
 cd /root
 cp /usr/share/man/man8/jail.8.gz /root/   # get my own copy of file.
 mv jail.8.gz ezjail.8.gz                  # rename the file.

 gunzip ezjail.8.gz                        # unzip the file.
 ee ezjail.8                               # edit the text file.


The start of the text file has the standard FreeBSD copyright comments. Delete all 
these comments. All groff_mdoc(7) documentation line macros begin with an period â€œ.â€ 
Then an uppercase letter followed by a lowercase letter. The following discussion 
has comments to the right and these comments are not part of the macro command syntax, 
but put here to explain whatâ€™s happening. So starting the new ezjail manpage text file is;


# Setup the manual format section.
Code:
.Dd July 22, 2010       # Date displayed on center of last line.
.Dt EZJAIL 8            # Name and section of this manpage, 
                        # has to be in uppercase letters,
                        # displays left & right corners of top line.
.Os                     # Displays RELEASE version in left & right
                        # corners of last line.



# This is how the man command displays the first and last lines.

Code:
EZJAIL(8)      FreeBSD System Manager's Manual       EZJAIL(8)

FreeBSD 8.0               July 22, 2010            FreeBSD 8.0


# Setup the highlighted first two lines you see.
Code:
.Sh NAME                # Section header name in uppercase letters.
.Nm ezjail              # Name to display.
.Nd â€œdescriptionâ€       # short description of command.


# This is what is displayed by the man command
Code:
NAME
     ezjail -- description


# Setup the command syntax section
Code:
.Sh SYNOPSIS            # Section header name in uppercase letters.
.Nm                     # Display saved name.
# The following macros format the flags in bold and/or with brackets
# and with white background / black letters. 
.Op Fl dhi              
.Op Fl J Ar jid_file
.Op Fl l u Ar username | Fl U Ar username
.Op Fl c | m
.Br
.Nm
.Op Fl hi
.Op Fl n Ar jailname
.Op Fl J Ar jid_file
.Op Fl s Ar securelevel
.Op Fl l u Ar username | Fl U Ar username
.Op Ar path hostname [ip[,..]] command ...


# This is what is displayed by the man command
Code:
SYNOPSIS
     jail [-dhi] [-J jid_file] [-l -u username | -U username] [-c | -m]
     jail [-hi] [-n jailname] [-J jid_file] [-s securelevel]
          [-l -u username | -U username] [path hostname [ip[,..]] 



# This is a real pain to play with. So I used the short method like this. 
It displays the text just as written with no bold and no white boxes. 
This method is simpler and makes the manpage easier to read without all 
those white-boxed words. The layout will be the same as what is shown above.


Code:
.Sh SYNOPSIS            
.Nm                       
[-dhi] [-J jid_file] [-l -u username | -U username] [-c | -m]
.Nm
[-hi] [-n jailname] [-J jid_file] [-s securelevel]
.Br                              # this means next line
[-l -u username | -U username] [path hostname [ip[,..]]



# The description section with the meaning of the flags comes next.
Code:
.Sh DESCRIPTION
The jail utility creates a new jail or modifies an existing jail, 
imprisoning the current process (and future descendants) inside it.
.Pp                            # blank line position holder.
The options are as follows:
.Bl -tag -width indent         # indent everything that follows.
.It Fl d                       # adds the dash and bolds them both.
Allow making changes to a dying jail.
.It Fl h                       # adds the dash and bolds them both.
Resolve the host.hostname parameter (or hostname) and add
all IP addresses returned by the resolver to the list of
ip addresses for this jail.  
.El                             # end the indented section.



# This is what is displayed by the man command
Code:
DESCRIPTION
     The jail utility creates a new jail or modifies an existing jail,
     optionally imprisoning the current process (and future
     descendants) inside it.

     The options are as follows:

     -d      Allow making changes to a dying jail.

     -h      Resolve the host.hostname parameter (or hostname) and add
             all IP addresses returned by the resolver to the list of
             ip addresses for this jail.



# The short method I used like this.
Code:
.Sh DESCRIPTION
The jail utility creates a new jail or modifies an existing jail, 
imprisoning the current process (and future descendants) inside it.
.Pp                            # blank line position holder
The options are as follows:
.Bl -tag -width indent         # indent everything that follows
.It \fB-d\fR                   # adds the bold 
Allow making changes to a dying jail.
.It \fB-h\fR                   # adds the bold 
Resolve the host.hostname parameter (or hostname) and add
all IP addresses returned by the resolver to the list of
ip addresses for this jail
.El                            # End the indented section.


# This is an example of the special enclosure macro that bolds any word 
or words its wrapped around. \fB 10.0.10.2 \fR will display as 10.0.10.2


General format notes.
The manual standards specify the following sections as mandatory. 

Code:
.Sh NAME
.Sh SYNOPSIS
.Sh DESCRIPTION

Which have been covered all ready. At the end of the manpage there are a 
few more mandatory sections required in all manpages.

Code:
.Sh FILES           # Section header name in uppercase letters.
/usr/local/etc/ezjail.conf
.br
/usr/local/bin/ezjail

.Sh SEE ALSO        # Section header name in uppercase letters.
.Xr killall 1 ,
.Xr lsvfs 1 ,
.Xr newaliases 1 ,
# or you could just say
killall(1), lsvfs(1), newaliases(1) 


.Sh AUTHORS         # Section header name in uppercase letters.
.An Tom Jones
.Aq tjones@home.com
# or you could just use
Tom Jones  tjones@home.com


Now in between the Description section and the FILES section you can make 
as many sections as you want by using the .Sh macro. Example

Code:
.Sh USAGE EXAMPLES
.Sh HISTORY
.Sh BACKGROUND

----------------------------------------------------------------------

http://man7.org/linux/man-pages/man7/groff_man.7.html

Groff Version 1.22.3     4 November 2014     GROFF_MAN(7)

GROFF_MAN(7)    Miscellaneous Information Manual     GROFF_MAN(7)
NAME         top

       groff_man - groff man macros to support generation of man pages
SYNOPSIS         top

       groff -man [options ...] [files ...]
       groff -m man [options ...] [files ...]
DESCRIPTION         top

       The man macros used to generate man pages with groff were written by
       James Clark.  This document provides a brief summary of the use of
       each macro in that package.
OPTIONS         top

       The man macros understand the following command line options (which
       define various registers).

       -rcR=1 This option (the default if in nroff mode) creates a single,
              very long page instead of multiple pages.  Say -rcR=0 to
              disable it.

       -rC1   If more than one manual page is given on the command line,
              number the pages continuously, rather than starting each at 1.

       -rD1   Double-sided printing.  Footers for even and odd pages are
              formatted differently.

       -rFT=dist
              Set distance of the footer relative to the bottom of the page
              if negative or relative to the top if positive.  The default
              is -0.5i.

       -rHY=flags
              Set hyphenation flags.  Possible values are 1 to hyphenate
              without restrictions, 2 to not hyphenate the last word on a
              page, 4 to not hyphenate the last two characters of a word,
              and 8 to not hyphenate the first two characters of a word.
              These values are additive; the default is 14.

       -rIN=width
              Set body text indentation to width.  The default is 7n for
              nroff, 7.2n for troff.  For nroff, this value should always be
              an integer multiple of unit ‘n’ to get consistent indentation.

       -rLL=line-length
              Set line length.  If this option is not given, the line length
              is set to respect any value set by a prior ‘.ll’ request
              (which must be in effect when the ‘.TH’ macro is invoked), if
              this differs from the built-in default for the formatter;
              otherwise it defaults to 78n in nroff mode and 6.5i in troff
              mode.

              Note that the use of a ‘.ll’ request to initialize the line
              length is supported for backward compatibility with some
              versions of the man program; direct initialization of the ‘LL’
              register should always be preferred to the use of such a
              request.  In particular, note that a ‘.ll 65n’ request does
              not preserve the normal nroff default line length, (the man
              default initialization to 78n prevails), whereas, the
              ‘-rLL=65n’ option, or an equivalent ‘.nr LL 65n’ request
              preceding the use of the ‘TH’ macro, does set a line length of
              65n.

       -rLT=title-length
              Set title length.  If this option is not given, the title
              length defaults to the line length.

       -rPnnn Enumeration of pages start with nnn rather than with 1.

       -rSxx  Base document font size is xx points (xx can be 10, 11, or 12)
              rather than 10 points.

       -rSN=width
              Set sub-subheading indentation to width.  The default is 3n.

       -rXnnn After page nnn, number pages as nnna, nnnb, nnnc, etc.  For
              example, the option ‘-rX2’ produces the following page
              numbers: 1, 2, 2a, 2b, 2c, etc.
USAGE         top

       This section describes the available macros for manual pages.  For
       further customization, put additional macros and requests into the
       file man.local, which is loaded immediately after the man package.

       .EX
       .EE    Example/End Example.  After .EX, filling is disabled and the
              font is set to constant-width.  This is useful for formatting
              code, command, and configuration-file examples.  The EE macro
              restores filling and restores the previous font.

              These macros are defined on many (but not all) legacy Unix
              systems running classic troff.  To be certain your page will
              be portable to those systems, copy their definitions from the
              an-ext.tmac file of a groff installation.

       .HP [nnn]
              Set up a paragraph with hanging left indentation.  The
              indentation is set to nnn if that argument is supplied (the
              default unit is ‘n’ if omitted), otherwise it is set to the
              previous indentation value specified with .TP, .IP, or .HP (or
              to the default value if none of them have been used yet).
              Font size and face are reset to its default values.  The
              following paragraph illustrates the effect of this macro with
              hanging indentation set to 4 (enclosed by .RS and .RE to set
              the left margin temporarily to the current indentation):

              This is a paragraph following an invocation of the HP macro.
                  As you can see, it produces a paragraph where all lines
                  but the first are indented.

              Use of this presentation-level macro is deprecated.  While it
              is universally portable to legacy Unix systems, a hanging
              indentation cannot be expressed naturally under HTML, and many
              HTML-based manual viewers simply interpret it as a starter for
              a normal paragraph.  Thus, any information or distinction you
              tried to express with the indentation may be lost.

       .IP [designator] [nnn]
              Set up an indented paragraph, using designator as a tag to
              mark its beginning.  The indentation is set to nnn if that
              argument is supplied (the default unit is ‘n’ if omitted),
              otherwise it is set to the previous indentation value
              specified with .TP, .IP, or .HP (or to the default value if
              none of them have been used yet).  Font size and face of the
              paragraph (but not the designator) are reset to its default
              values.

              To start an indented paragraph with a particular indentation
              but without a designator, use ‘""’ (two doublequotes) as the
              second argument.

              For example, the following paragraphs were all set up with
              bullets as the designator, using ‘.IP \(bu 4’.  The whole
              block has been enclosed with .RS and .RE to set the left
              margin temporarily to the current indentation value.

              ·   IP is one of the three macros used in the man package to
                  format lists.

              ·   HP is another.  This macro produces a paragraph with a
                  left hanging indentation.

              ·   TP is another.  This macro produces an unindented label
                  followed by an indented paragraph.

       .LP
       .PP
       .P     These macros are mutual aliases.  Any of them causes a line
              break at the current position, followed by a vertical space
              downwards by the amount specified by the PD macro.  The font
              size and shape are reset to the default value (normally 10pt
              Roman).  Finally, the current left margin and the indentation
              is reset to the default values.

       .RE [nnn]
              This macro moves the left margin back to level nnn, restoring
              the previous left margin.  If no argument is given, it moves
              one level back.  The first level (i.e., no call to .RS yet)
              has number 1, and each call to .RS increases the level by 1.

       .RS [nnn]
              This macro moves the left margin to the right by the value nnn
              if specified (default unit is ‘n’); otherwise it is set to the
              previous indentation value specified with .TP, .IP, or .HP (or
              to the default value if none of them have been used yet).  The
              indentation value is then set to the default.

              Calls to the RS macro can be nested.

       .SH [text for a heading]
              Set up an unnumbered section heading sticking out to the left.
              Prints out all the text following .SH up to the end of the
              line (or the text in the next input line if there is no
              argument to .SH) in bold face (or the font specified by the
              string HF), one size larger than the base document size.
              Additionally, the left margin and the indentation for the
              following text is reset to the default values.

       .SS [text for a heading]
              Set up a secondary, unnumbered section heading.  Prints out
              all the text following .SS up to the end of the line (or the
              text in the next input line if there is no argument to .SS) in
              bold face (or the font specified by the string HF), at the
              same size as the base document size.  Additionally, the left
              margin and the indentation for the following text is reset to
              the default values.

       .TH title section [extra1] [extra2] [extra3]
              Set the title of the man page to title and the section to
              section, which must take on a value between 1 and 8.  The
              value section may also have a string appended, e.g. ‘.pm’, to
              indicate a specific subsection of the man pages.  Both title
              and section are positioned at the left and right in the header
              line (with section in parentheses immediately appended to
              title.  extra1 is positioned in the middle of the footer line.
              extra2 is positioned at the left in the footer line (or at the
              left on even pages and at the right on odd pages if double-
              sided printing is active).  extra3 is centered in the header
              line.

              For HTML output, headers and footers are completely
              suppressed.

              Additionally, this macro starts a new page; the new line
              number is 1 again (except if the ‘-rC1’ option is given on the
              command line) -- this feature is intended only for formatting
              multiple man pages; a single man page should contain exactly
              one TH macro at the beginning of the file.

       .TP [nnn]
              Set up an indented paragraph with label.  The indentation is
              set to nnn if that argument is supplied (the default unit is
              ‘n’ if omitted), otherwise it is set to the previous
              indentation value specified with .TP, .IP, or .HP (or to the
              default value if none of them have been used yet).

              The first input line of text following this macro is
              interpreted as a string to be printed flush-left, as it is
              appropriate for a label.  It is not interpreted as part of a
              paragraph, so there is no attempt to fill the first line with
              text from the following input lines.  Nevertheless, if the
              label is not as wide as the indentation the paragraph starts
              at the same line (but indented), continuing on the following
              lines.  If the label is wider than the indentation the
              descriptive part of the paragraph begins on the line following
              the label, entirely indented.  Note that neither font shape
              nor font size of the label is set to a default value; on the
              other hand, the rest of the text has default font settings.

              The TP macro is the macro used for the explanations you are
              just reading.

       .TQ    The TQ macro sets up header continuation for a TP macro.  With
              it, you can stack up any number of labels (such as in a
              glossary, or list of commands) before beginning the indented
              paragraph.  For an example, look up the documentation of the
              LP, PP, and P macros.

              This macro is not defined on legacy Unix systems running
              classic troff.  To be certain your page will be portable to
              those systems, copy its definition from the an-ext.tmac file
              of a groff installation.

       To summarize, the following macros cause a line break with the
       insertion of vertical space (which amount can be changed with the PD
       macro): SH, SS, TP, TQ, LP (PP, P), IP, and HP.  The macros RS, RE,
       EX, and EE also cause a break but no insertion of vertical space.
MACROS TO SET FONTS         top

       The standard font is Roman; the default text size is 10 point.

       .B [text]
              Causes text to appear in bold face.  If no text is present on
              the line where the macro is called the text of the next input
              line appears in bold face.

       .BI text
              Causes text on the same line to appear alternately in bold
              face and italic.  The text must be on the same line as the
              macro call.  Thus

                     .BI this "word and" that

              would cause ‘this’ and ‘that’ to appear in bold face, while
              ‘word and’ appears in italics.

       .BR text
              Causes text on the same line to appear alternately in bold
              face and roman.  The text must be on the same line as the
              macro call.

       .I [text]
              Causes text to appear in italic.  If no text is present on the
              line where the macro is called the text of the next input line
              appears in italic.

       .IB text
              Causes text to appear alternately in italic and bold face.
              The text must be on the same line as the macro call.

       .IR text
              Causes text on the same line to appear alternately in italic
              and roman.  The text must be on the same line as the macro
              call.

       .RB text
              Causes text on the same line to appear alternately in roman
              and bold face.  The text must be on the same line as the macro
              call.

       .RI text
              Causes text on the same line to appear alternately in roman
              and italic.  The text must be on the same line as the macro
              call.

       .SB [text]
              Causes the text on the same line or the text on the next input
              line to appear in boldface font, one point size smaller than
              the default font.

       .SM [text]
              Causes the text on the same line or the text on the next input
              line to appear in a font that is one point size smaller than
              the default font.
MACROS TO DESCRIBE HYPERLINKS AND EMAIL ADDRESSES         top

       The following macros are not defined on legacy Unix systems running
       classic troff.  To be certain your page will be portable to those
       systems, copy their definitions from the an-ext.tmac file of a groff
       installation.

       Using these macros helps ensure that you get hyperlinks when your
       manual page is rendered in a browser or other program that is Web-
       enabled.

       .MT address
       .ME [punctuation]
              Wrap an email address.  The argument of .MT is the address;
              text following, until .ME, is a name to be associated with the
              address.  Any argument to the ME macro is pasted to the end of
              the link text.  On a device that is not a browser,

                     contact
                     .MT fred.foonly@\:fubar.net
                     Fred Foonly
                     .ME
                     for more information

              usually displays like this: “contact Fred Foonly <fred.foonly@
              fubar.net> for more information”.

              The use of \: to insert hyphenless breakpoints is a groff
              extension and can be omitted.

       .UR URL
       .UE [punctuation]
              Wrap a World Wide Web hyperlink.  The argument to .UR is the
              URL; thereafter, lines until .UE are collected and used as the
              link text.  Any argument to the UE macro is pasted to the end
              of the text.  On a device that is not a browser,

                     this is a link to
                     .UR http://\:randomsite.org/\:fubar
                     some random site
                     .UE ,
                     given as an example

              usually displays like this: “this is a link to some random
              site <http://randomsite.org/fubar>, given as an example”.

              The use of \: to insert hyphenless breakpoints is a groff
              extension and can be omitted.
MACROS TO DESCRIBE COMMAND SYNOPSES         top

       The following macros are not defined on legacy Unix systems running
       classic troff.  To be certain your page will be portable to those
       systems, copy their definitions from the an-ext.tmac file of a groff
       installation.

       These macros are a convenience for authors.  They also assist
       automated translation tools and help browsers in recognizing command
       synopses and treating them differently from running text.

       .OP key value
              Describe an optional command argument.  The arguments of this
              macro are set surrounded by option braces in the default Roman
              font; the first argument is printed with a bold face, while
              the second argument is typeset as italic.

       .SY command
              Begin synopsis.  Takes a single argument, the name of a
              command.  Text following, until closed by .YS, is set with a
              hanging indentation with the width of command plus a space.
              This produces the traditional look of a Unix command synopsis.

       .YS    This macro restores normal indentation at the end of a command
              synopsis.

       Here is a real example:

              .SY groff
              .OP \-abcegiklpstzCEGNRSUVXZ
              .OP \-d cs
              .OP \-f fam
              .OP \-F dir
              .OP \-I dir
              .OP \-K arg
              .OP \-L arg
              .OP \-m name
              .OP \-M dir
              .OP \-n num
              .OP \-o list
              .OP \-P arg
              .OP \-r cn
              .OP \-T dev
              .OP \-w name
              .OP \-W name
              .RI [ file
              .IR .\|.\|. ]
              .YS

       produces the following output:

              groff [-abcegiklpstzCEGNRSUVXZ] [-d cs] [-f fam] [-F dir]
                    [-I dir] [-K arg] [-L arg] [-m name] [-M dir] [-n num]
                    [-o list] [-P arg] [-r cn] [-T dev] [-w name] [-W name]
                    [file ...]

       If necessary, you might use br requests to control line breaking.
       You can insert plain text as well; this looks like the traditional
       (unornamented) syntax for a required command argument or filename.
MISCELLANEOUS         top

       The default indentation is 7.2n in troff mode and 7n in nroff mode
       except for grohtml, which ignores indentation.

       .AT [system [release]]
              Alter the footer for use with AT&T man pages.  This command
              exists only for compatibility; don't use it.  See the groff
              info manual for more.

       .BT    Print the footer string.  Redefine this macro to get control
              of the footer.

       .DT    Set tabs every 0.5 inches.  Since this macro is always called
              during a TH macro, it makes sense to call it only if the tab
              positions have been changed.

              Use of this presentation-level macro is deprecated.  It
              translates poorly to HTML, under which exact whitespace
              control and tabbing are not readily available.  Thus,
              information or distinctions that you use .DT to express are
              likely to be lost.  If you feel tempted to use it, you should
              probably be composing a table using tbl(1) markup instead.

       .PD [nnn]
              Adjust the empty space before a new paragraph or section.  The
              optional argument gives the amount of space (default unit is
              ‘v’); without parameter, the value is reset to its default
              value (1 line in nroff mode, 0.4v otherwise).  This affects
              the macros SH, SS, TP, LP (resp. PP and P), IP, and HP.

              Use of this presentation-level macro is deprecated.  It
              translates poorly to HTML, under which exact control of inter-
              paragraph spacing is not readily available.  Thus, information
              or distinctions that you use .PD to express are likely to be
              lost.

       .PT    Print the header string.  Redefine this macro to get control
              of the header.

       .UC [version]
              Alter the footer for use with BSD man pages.  This command
              exists only for compatibility; don't use it.  See the groff
              info manual for more.

       The following strings are defined:

       \*R    The ‘registered’ sign.

       \*S    Switch back to the default font size.

       \*(lq
       \*(rq  Left and right quote.  This is equal to ‘\(lq’ and ‘\(rq\[cq],
              respectively.

       \*(HF  The typeface used to print headings and subheadings.  The
              default is ‘B’.

       \*(Tm  The ‘trademark’ sign.

       If a preprocessor like tbl or eqn is needed, it has become common to
       make the first line of the man page look like this:

              '\" word

       Note the single space character after the double quote.  word
       consists of letters for the needed preprocessors: ‘e’ for eqn, ‘r’
       for refer, and ‘t’ for tbl.  Modern implementations of the man
       program read this first line and automatically call the right
       preprocessor(s).
PORTABILITY AND TROFF REQUESTS         top

       Since the man macros consist of groups of groff requests, one can, in
       principle, supplement the functionality of the man macros with
       individual groff requests where necessary.  See the groff info pages
       for a complete reference of all requests.

       Note, however, that using raw troff requests is likely to make your
       page render poorly on the (increasingly common) class of viewers that
       render it to HTML.  Troff requests make implicit assumptions about
       things like character and page sizes that may break in an HTML
       environment; also, many of these viewers don't interpret the full
       troff vocabulary, a problem that can lead to portions of your text
       being silently dropped.

       For portability to modern viewers, it is best to write your page
       entirely in the requests described on this page.  Further, it is best
       to completely avoid those we have described as ‘presentation-level’
       (.HP, .PD, and .DT).

       The macros we have described as extensions (.EX/.EE, .SY/.OP/.YS,
       .UR/.UE, and .MT/.ME) should be used with caution, as they may not
       yet be built in to some viewer that is important to your audience.
       If in doubt, copy the implementation onto your page.
FILES         top

       man.tmac
       an.tmac
              These are wrapper files to call andoc.tmac.

       andoc.tmac
              Use this file in case you don't know whether the man macros or
              the mdoc package should be used.  Multiple man pages (in
              either format) can be handled.

       an-old.tmac
              Most man macros are contained in this file.

       an-ext.tmac
              The extension macro definitions for .SY, .OP, .YS, .TQ,
              .EX/.EE, .UR/.UE, and .MT/.ME are contained in this file.  It
              is written in classic troff, and released for free re-use, and
              not copylefted; manual page authors concerned about
              portability to legacy Unix systems are encouraged to copy
              these definitions into their pages, and maintainers of troff
              or its workalikes are encouraged to re-use them.

              Note that the definitions for these macros are read after the
              call of TH, so they will replace macros of the same names
              given at the beginning of your file.  If you must use your own
              definitions for these macros, they must be given after calling
              TH.

       man.local
              Local changes and customizations should be put into this file.
SEE ALSO         top

       tbl(1), eqn(1), refer(1), man(1), man(7), groff_mdoc(7)
COPYING         top

       Copyright © 1999-2014 Free Software Foundation, Inc.

       Permission is granted to make and distribute verbatim copies of this
       manual provided the copyright notice and this permission notice are
       preserved on all copies.

       Permission is granted to copy and distribute modified versions of
       this manual under the conditions for verbatim copying, provided that
       the entire resulting derived work is distributed under the terms of a
       permission notice identical to this one.

       Permission is granted to copy and distribute translations of this
       manual into another language, under the above conditions for modified
       versions, except that this permission notice may be included in
       translations approved by the Free Software Foundation instead of in
       the original English.
AUTHORS         top

       This manual page was originally written for the Debian GNU/Linux
       system by Susan G. Kleinmann ⟨sgk@debian.org⟩.

       It was corrected and updated by Werner Lemberg ⟨wl@gnu.org⟩.

       The extension macros were documented (and partly designed) by Eric S.
       Raymond ⟨esr@thyrsus.com⟩; he also wrote the portability advice.
COLOPHON         top

       This page is part of the groff (GNU troff) project.  Information
       about the project can be found at 
       ⟨http://www.gnu.org/software/groff/⟩.  If you have a bug report for
       this manual page, see ⟨http://www.gnu.org/software/groff/⟩.  This
       page was obtained from the tarball groff-1.22.3.tar.gz fetched from
       ⟨ftp://ftp.gnu.org/gnu/groff/⟩ on 2016-12-10.  If you discover any
       rendering problems in this HTML version of the page, or you believe
       there is a better or more up-to-date source for the page, or you have
       corrections or improvements to the information in this COLOPHON
       (which is not part of the original manual page), send a mail to
       man-pages@man7.org

----------------------------------------------------------------------

# man mdoc

MDOC(7)            FreeBSD Miscellaneous Information Manual            MDOC(7)                  
                                                                                                
NAME                                                                                            
     mdoc – semantic markup language for formatting manual pages                                
                                                                                                
DESCRIPTION                                                                                     
     The mdoc language supports authoring of manual pages for the man(1)                        
     utility by allowing semantic annotations of words, phrases, page sections                  
     and complete manual pages.  Such annotations are used by formatting tools                  
     to achieve a uniform presentation across all manuals written in mdoc, and                  
     to support hyperlinking if supported by the output medium.                                 
                                                                                                
     This reference document describes the structure of manual pages and the                    
     syntax and usage of the mdoc language.  The reference implementation of a                  
     parsing and formatting tool is mandoc(1); the COMPATIBILITY section                        
     describes compatibility with other implementations.                                        
                                                                                                
     In an mdoc document, lines beginning with the control character ‘.’ are                    
     called “macro lines”.  The first word is the macro name.  It consists of                   
     two or three letters.  Most macro names begin with a capital letter.  For                  
     a list of available macros, see MACRO OVERVIEW.  The words following the                   
     macro name are arguments to the macro, optionally including the names of                   
     other, callable macros; see MACRO SYNTAX for details.                                      
                                                                                                
     Lines not beginning with the control character are called “text lines”.                    
     They provide free-form text to be printed; the formatting of the text                      
     depends on the respective processing context:                                              
                                                                                                
           .Sh Macro lines change control state.                                                
           Text lines are interpreted within the current state.                                 

     Many aspects of the basic syntax of the mdoc language are based on the
     roff(7) language; see the LANGUAGE SYNTAX and MACRO SYNTAX sections in
     the roff(7) manual for details, in particular regarding comments, escape
     sequences, whitespace, and quoting.  However, using roff(7) requests in
     mdoc documents is discouraged; mandoc(1) supports some of them merely for
     backward compatibility.

MANUAL STRUCTURE
     A well-formed mdoc document consists of a document prologue followed by
     one or more sections.

     The prologue, which consists of the Dd, Dt, and Os macros in that order,
     is required for every document.

     The first section (sections are denoted by Sh) must be the NAME section,
     consisting of at least one Nm followed by Nd.

     Following that, convention dictates specifying at least the SYNOPSIS and
     DESCRIPTION sections, although this varies between manual sections.

     The following is a well-formed skeleton mdoc file for a utility
     "progname":

           .Dd $Mdocdate$
           .Dt PROGNAME section
           .Os
           .Sh NAME
           .Nm progname
           .Nd one line about what it does
           .\" .Sh LIBRARY
           .\" For sections 2, 3, and 9 only.
           .\" Not used in OpenBSD.
           .Sh SYNOPSIS
           .Nm progname
           .Op Fl options
           .Ar
           .Sh DESCRIPTION
           The
           .Nm
           utility processes files ...
           .\" .Sh CONTEXT
           .\" For section 9 functions only.
           .\" .Sh IMPLEMENTATION NOTES
           .\" Not used in OpenBSD.
           .\" .Sh RETURN VALUES
           .\" For sections 2, 3, and 9 function return values only.
           .\" .Sh ENVIRONMENT
           .\" For sections 1, 6, 7, and 8 only.
           .\" .Sh FILES
           .\" .Sh EXIT STATUS
           .\" For sections 1, 6, and 8 only.
           .\" .Sh EXAMPLES
           .\" .Sh DIAGNOSTICS
           .\" For sections 1, 4, 6, 7, 8, and 9 printf/stderr messages only.
           .\" .Sh ERRORS
           .\" For sections 2, 3, 4, and 9 errno settings only.
           .\" .Sh SEE ALSO
           .\" .Xr foobar 1
           .\" .Sh STANDARDS
           .\" .Sh HISTORY
           .\" .Sh AUTHORS
           .\" .Sh CAVEATS
           .\" .Sh BUGS
           .\" .Sh SECURITY CONSIDERATIONS
           .\" Not used in OpenBSD.

     The sections in an mdoc document are conventionally ordered as they
     appear above.  Sections should be composed as follows:

           NAME
           The name(s) and a one line description of the documented material.
           The syntax for this as follows:

                 .Nm name0 ,
                 .Nm name1 ,
                 .Nm name2
                 .Nd a one line description

           Multiple ‘Nm’ names should be separated by commas.

           The Nm macro(s) must precede the Nd macro.

           See Nm and Nd.

           LIBRARY
           The name of the library containing the documented material, which
           is assumed to be a function in a section 2, 3, or 9 manual.  The
           syntax for this is as follows:

                 .Lb libarm

           See Lb.

           SYNOPSIS
           Documents the utility invocation syntax, function call syntax, or
           device configuration.

           For the first, utilities (sections 1, 6, and 8), this is generally
           structured as follows:

                 .Nm bar
                 .Op Fl v
                 .Op Fl o Ar file
                 .Op Ar
                 .Nm foo
                 .Op Fl v
                 .Op Fl o Ar file
                 .Op Ar

           Commands should be ordered alphabetically.

           For the second, function calls (sections 2, 3, 9):

                 .In header.h
                 .Vt extern const char *global;
                 .Ft "char *"
                 .Fn foo "const char *src"
                 .Ft "char *"
                 .Fn bar "const char *src"

           Ordering of In, Vt, Fn, and Fo macros should follow C header-file
           conventions.

           And for the third, configurations (section 4):

                 .Cd "it* at isa? port 0x2e"
                 .Cd "it* at isa? port 0x4e"

           Manuals not in these sections generally don't need a SYNOPSIS.

           Some macros are displayed differently in the SYNOPSIS section,
           particularly Nm, Cd, Fd, Fn, Fo, In, Vt, and Ft.  All of these
           macros are output on their own line.  If two such dissimilar macros
           are pairwise invoked (except for Ft before Fo or Fn), they are
           separated by a vertical space, unless in the case of Fo, Fn, and
           Ft, which are always separated by vertical space.

           When text and macros following an Nm macro starting an input line
           span multiple output lines, all output lines but the first will be
           indented to align with the text immediately following the Nm macro,
           up to the next Nm, Sh, or Ss macro or the end of an enclosing
           block, whichever comes first.

           DESCRIPTION
           This begins with an expansion of the brief, one line description in
           NAME:

                 The
                 .Nm
                 utility does this, that, and the other.

           It usually follows with a breakdown of the options (if documenting
           a command), such as:

                 The arguments are as follows:
                 .Bl -tag -width Ds
                 .It Fl v
                 Print verbose information.
                 .El

           List the options in alphabetical order, uppercase before lowercase
           for each letter and with no regard to whether an option takes an
           argument.  Put digits in ascending order before all letter options.

           Manuals not documenting a command won't include the above fragment.

           Since the DESCRIPTION section usually contains most of the text of
           a manual, longer manuals often use the Ss macro to form
           subsections.  In very long manuals, the DESCRIPTION may be split
           into multiple sections, each started by an Sh macro followed by a
           non-standard section name, and each having several subsections,
           like in the present mdoc manual.

           CONTEXT
           This section lists the contexts in which functions can be called in
           section 9.  The contexts are autoconf, process, or interrupt.

           IMPLEMENTATION NOTES
           Implementation-specific notes should be kept here.  This is useful
           when implementing standard functions that may have side effects or
           notable algorithmic implications.

           RETURN VALUES
           This section documents the return values of functions in sections
           2, 3, and 9.

           See Rv.

           ENVIRONMENT
           Lists the environment variables used by the utility, and explains
           the syntax and semantics of their values.  The environ(7) manual
           provides examples of typical content and formatting.

           See Ev.

           FILES
           Documents files used.  It's helpful to document both the file name
           and a short description of how the file is used (created, modified,
           etc.).

           See Pa.

           EXIT STATUS
           This section documents the command exit status for section 1, 6,
           and 8 utilities.  Historically, this information was described in
           DIAGNOSTICS, a practise that is now discouraged.

           See Ex.

           EXAMPLES
           Example usages.  This often contains snippets of well-formed, well-
           tested invocations.  Make sure that examples work properly!

           DIAGNOSTICS
           Documents error messages.  In section 4 and 9 manuals, these are
           usually messages printed by the kernel to the console and to the
           kernel log.  In section 1, 6, 7, and 8, these are usually messages
           printed by userland programs to the standard error output.

           Historically, this section was used in place of EXIT STATUS for
           manuals in sections 1, 6, and 8; however, this practise is
           discouraged.

           See Bl -diag.

           ERRORS
           Documents errno(2) settings in sections 2, 3, 4, and 9.

           See Er.

           SEE ALSO
           References other manuals with related topics.  This section should
           exist for most manuals.  Cross-references should conventionally be
           ordered first by section, then alphabetically (ignoring case).

           References to other documentation concerning the topic of the
           manual page, for example authoritative books or journal articles,
           may also be provided in this section.

           See Rs and Xr.

           STANDARDS
           References any standards implemented or used.  If not adhering to
           any standards, the HISTORY section should be used instead.

           See St.

           HISTORY
           A brief history of the subject, including where it was first
           implemented, and when it was ported to or reimplemented for the
           operating system at hand.

           AUTHORS
           Credits to the person or persons who wrote the code and/or
           documentation.  Authors should generally be noted by both name and
           email address.

           See An.

           CAVEATS
           Common misuses and misunderstandings should be explained in this
           section.

           BUGS
           Known bugs, limitations, and work-arounds should be described in
           this section.

           SECURITY CONSIDERATIONS
           Documents any security precautions that operators should consider.

MACRO OVERVIEW
     This overview is sorted such that macros of similar purpose are listed
     together, to help find the best macro for any given purpose.  Deprecated
     macros are not included in the overview, but can be found below in the
     alphabetical MACRO REFERENCE.

   Document preamble and NAME section macros
     Dd               document date: $Mdocdate$ | month day, year
     Dt               document title: TITLE section [arch]
     Os               operating system version: [system [version]]
     Nm               document name (one argument)
     Nd               document description (one line)

   Sections and cross references
     Sh               section header (one line)
     Ss               subsection header (one line)
     Sx               internal cross reference to a section or subsection
     Xr               cross reference to another manual page: name section
     Pp, Lp           start a text paragraph (no arguments)

   Displays and lists
     Bd, Ed           display block: -type [-offset width] [-compact]
     D1               indented display (one line)
     Dl               indented literal display (one line)
     Ql               in-line literal display: ‘text’
     Bl, El           list block: -type [-width val] [-offset val] [-compact]
     It               list item (syntax depends on -type)
     Ta               table cell separator in Bl -column lists
     Rs, %*, Re       bibliographic block (references)

   Spacing control
     Pf               prefix, no following horizontal space (one argument)
     Ns               roman font, no preceding horizontal space (no arguments)
     Ap               apostrophe without surrounding whitespace (no arguments)
     Sm               switch horizontal spacing mode: [on | off]
     Bk, Ek           keep block: -words
     br               force output line break in text mode (no arguments)
     sp               force vertical space: [height]

   Semantic markup for command line utilities:
     Nm               start a SYNOPSIS block with the name of a utility
     Fl               command line options (flags) (>=0 arguments)
     Cm               command modifier (>0 arguments)
     Ar               command arguments (>=0 arguments)
     Op, Oo, Oc       optional syntax elements (enclosure)
     Ic               internal or interactive command (>0 arguments)
     Ev               environmental variable (>0 arguments)
     Pa               file system path (>=0 arguments)

   Semantic markup for function libraries:
     Lb               function library (one argument)
     In               include file (one argument)
     Fd               other preprocessor directive (>0 arguments)
     Ft               function type (>0 arguments)
     Fo, Fc           function block: funcname
     Fn               function name: [functype] funcname [[argtype] argname]
     Fa               function argument (>0 arguments)
     Vt               variable type (>0 arguments)
     Va               variable name (>0 arguments)
     Dv               defined variable or preprocessor constant (>0 arguments)
     Er               error constant (>0 arguments)
     Ev               environmental variable (>0 arguments)

   Various semantic markup:
     An               author name (>0 arguments)
     Lk               hyperlink: uri [name]
     Mt               “mailto” hyperlink: address
     Cd               kernel configuration declaration (>0 arguments)
     Ad               memory address (>0 arguments)
     Ms               mathematical symbol (>0 arguments)

   Physical markup
     Em               italic font or underline (emphasis) (>0 arguments)
     Sy               boldface font (symbolic) (>0 arguments)
     Li               typewriter font (literal) (>0 arguments)
     No               return to roman font (normal) (no arguments)
     Bf, Ef           font block: [-type | Em | Li | Sy]

   Physical enclosures
     Dq, Do, Dc       enclose in typographic double quotes: “text”
     Qq, Qo, Qc       enclose in typewriter double quotes: "text"
     Sq, So, Sc       enclose in single quotes: ‘text’
     Pq, Po, Pc       enclose in parentheses: (text)
     Bq, Bo, Bc       enclose in square brackets: [text]
     Brq, Bro, Brc    enclose in curly braces: {text}
     Aq, Ao, Ac       enclose in angle brackets: ⟨text⟩
     Eo, Ec           generic enclosure

   Text production
     Ex -std          standard command exit values: [utility ...]
     Rv -std          standard function return values: [function ...]
     St               reference to a standards document (one argument)
     At               AT&T UNIX
     Bx               BSD
     Bsx              BSD/OS
     Nx               NetBSD
     Fx               FreeBSD
     Ox               OpenBSD
     Dx               DragonFly

MACRO REFERENCE
     This section is a canonical reference of all macros, arranged
     alphabetically.  For the scoping of individual macros, see MACRO SYNTAX.

   %A
     Author name of an Rs block.  Multiple authors should each be accorded
     their own %A line.  Author names should be ordered with full or
     abbreviated forename(s) first, then full surname.

   %B
     Book title of an Rs block.  This macro may also be used in a non-
     bibliographic context when referring to book titles.

   %C
     Publication city or location of an Rs block.

   %D
     Publication date of an Rs block.  Recommended formats of arguments are
     month day, year or just year.

   %I
     Publisher or issuer name of an Rs block.

   %J
     Journal name of an Rs block.

   %N
     Issue number (usually for journals) of an Rs block.

   %O
     Optional information of an Rs block.

   %P
     Book or journal page number of an Rs block.

   %Q
     Institutional author (school, government, etc.) of an Rs block.  Multiple
     institutional authors should each be accorded their own %Q line.

   %R
     Technical report name of an Rs block.

   %T
     Article title of an Rs block.  This macro may also be used in a non-
     bibliographical context when referring to article titles.

   %U
     URI of reference document.

   %V
     Volume number of an Rs block.

   Ac
     Close an Ao block.  Does not have any tail arguments.

   Ad
     Memory address.  Do not use this for postal addresses.

     Examples:
           .Ad [0,$]
           .Ad 0x00000000

   An
     Author name.  Can be used both for the authors of the program, function,
     or driver documented in the manual, or for the authors of the manual
     itself.  Requires either the name of an author or one of the following
     arguments:

           -split     Start a new output line before each subsequent
                      invocation of An.
           -nosplit   The opposite of -split.

     The default is -nosplit.  The effect of selecting either of the -split
     modes ends at the beginning of the AUTHORS section.  In the AUTHORS
     section, the default is -nosplit for the first author listing and -split
     for all other author listings.

     Examples:
           .An -nosplit
           .An Kristaps Dzonsons Aq Mt kristaps@bsd.lv

   Ao
     Begin a block enclosed by angle brackets.  Does not have any head
     arguments.

     Examples:
           .Fl -key= Ns Ao Ar val Ac

     See also Aq.

   Ap
     Inserts an apostrophe without any surrounding whitespace.  This is
     generally used as a grammatical device when referring to the verb form of
     a function.

     Examples:
           .Fn execve Ap d

   Aq
     Encloses its arguments in angle brackets.

     Examples:
           .Fl -key= Ns Aq Ar val

     Remarks: this macro is often abused for rendering URIs, which should
     instead use Lk or Mt, or to note pre-processor “#include” statements,
     which should use In.

     See also Ao.

   Ar
     Command arguments.  If an argument is not provided, the string “file ...”
     is used as a default.

     Examples:
           .Fl o Ar file
           .Ar
           .Ar arg1 , arg2 .

     The arguments to the Ar macro are names and placeholders for command
     arguments; for fixed strings to be passed verbatim as arguments, use Fl
     or Cm.

   At
     Formats an AT&T UNIX version.  Accepts one optional argument:

           v[1-7] | 32v   A version of AT&T UNIX.
           III            AT&T System III UNIX.
           V[.[1-4]]?     A version of AT&T System V UNIX.

     Note that these arguments do not begin with a hyphen.

     Examples:
           .At
           .At III
           .At V.1

     See also Bsx, Bx, Dx, Fx, Nx, and Ox.

   Bc
     Close a Bo block.  Does not have any tail arguments.

   Bd
     Begin a display block.  Its syntax is as follows:

           .Bd -type [-offset width] [-compact]

     Display blocks are used to select a different indentation and
     justification than the one used by the surrounding text.  They may
     contain both macro lines and text lines.  By default, a display block is
     preceded by a vertical space.

     The type must be one of the following:

           -centered      Produce one output line from each input line, and
                          center-justify each line.  Using this display type
                          is not recommended; many mdoc implementations render
                          it poorly.

           -filled        Change the positions of line breaks to fill each
                          line, and left- and right-justify the resulting
                          block.

           -literal       Produce one output line from each input line, and do
                          not justify the block at all.  Preserve white space
                          as it appears in the input.  Always use a constant-
                          width font.  Use this for displaying source code.

           -ragged        Change the positions of line breaks to fill each
                          line, and left-justify the resulting block.

           -unfilled      The same as -literal, but using the same font as for
                          normal text, which is a variable width font if
                          supported by the output device.

     The type must be provided first.  Additional arguments may follow:

           -offset width  Indent the display by the width, which may be one of
                          the following:

                          One of the pre-defined strings indent, the width of
                          a standard indentation (six constant width
                          characters); indent-two, twice indent; left, which
                          has no effect; right, which justifies to the right
                          margin; or center, which aligns around an imagined
                          center axis.

                          A macro invocation, which selects a predefined width
                          associated with that macro.  The most popular is the
                          imaginary macro Ds, which resolves to 6n.

                          A scaling width as described in roff(7).

                          An arbitrary string, which indents by the length of
                          this string.

                          When the argument is missing, -offset is ignored.

           -compact       Do not assert vertical space before the display.

     Examples:

           .Bd -literal -offset indent -compact
              Hello       world.
           .Ed

     See also D1 and Dl.

   Bf
     Change the font mode for a scoped block of text.  Its syntax is as
     follows:

           .Bf [-emphasis | -literal | -symbolic | Em | Li | Sy]

     The -emphasis and Em argument are equivalent, as are -symbolic and Sy,
     and -literal and Li.  Without an argument, this macro does nothing.  The
     font mode continues until broken by a new font mode in a nested scope or
     Ef is encountered.

     See also Li, Ef, Em, and Sy.

   Bk
     For each macro, keep its output together on the same output line, until
     the end of the macro or the end of the input line is reached, whichever
     comes first.  Line breaks in text lines are unaffected.  The syntax is as
     follows:

           .Bk -words

     The -words argument is required; additional arguments are ignored.

     The following example will not break within each Op macro line:

           .Bk -words
           .Op Fl f Ar flags
           .Op Fl o Ar output
           .Ek

     Be careful in using over-long lines within a keep block!  Doing so will
     clobber the right margin.

   Bl
     Begin a list.  Lists consist of items specified using the It macro,
     containing a head or a body or both.  The list syntax is as follows:

           .Bl -type [-width val] [-offset val] [-compact] [HEAD ...]

     The list type is mandatory and must be specified first.  The -width and
     -offset arguments accept macro names as described for Bd -offset, scaling
     widths as described in roff(7), or use the length of the given string.
     The -offset is a global indentation for the whole list, affecting both
     item heads and bodies.  For those list types supporting it, the -width
     argument requests an additional indentation of item bodies, to be added
     to the -offset.  Unless the -compact argument is specified, list entries
     are separated by vertical space.

     A list must specify one of the following list types:

           -bullet       No item heads can be specified, but a bullet will be
                         printed at the head of each item.  Item bodies start
                         on the same output line as the bullet and are
                         indented according to the -width argument.

           -column       A columnated list.  The -width argument has no
                         effect; instead, each argument specifies the width of
                         one column, using either the scaling width syntax
                         described in roff(7) or the string length of the
                         argument.  If the first line of the body of a -column
                         list is not an It macro line, It contexts spanning
                         one input line each are implied until an It macro
                         line is encountered, at which point items start being
                         interpreted as described in the It documentation.

           -dash         Like -bullet, except that dashes are used in place of
                         bullets.

           -diag         Like -inset, except that item heads are not parsed
                         for macro invocations.  Most often used in the
                         DIAGNOSTICS section with error constants in the item
                         heads.

           -enum         A numbered list.  No item heads can be specified.
                         Formatted like -bullet, except that cardinal numbers
                         are used in place of bullets, starting at 1.

           -hang         Like -tag, except that the first lines of item bodies
                         are not indented, but follow the item heads like in
                         -inset lists.

           -hyphen       Synonym for -dash.

           -inset        Item bodies follow items heads on the same line,
                         using normal inter-word spacing.  Bodies are not
                         indented, and the -width argument is ignored.

           -item         No item heads can be specified, and none are printed.
                         Bodies are not indented, and the -width argument is
                         ignored.

           -ohang        Item bodies start on the line following item heads
                         and are not indented.  The -width argument is
                         ignored.

           -tag          Item bodies are indented according to the -width
                         argument.  When an item head fits inside the
                         indentation, the item body follows this head on the
                         same output line.  Otherwise, the body starts on the
                         output line following the head.

     Lists may be nested within lists and displays.  Nesting of -column and
     -enum lists may not be portable.

     See also El and It.

   Bo
     Begin a block enclosed by square brackets.  Does not have any head
     arguments.

     Examples:
           .Bo 1 ,
           .Dv BUFSIZ Bc

     See also Bq.

   Bq
     Encloses its arguments in square brackets.

     Examples:
           .Bq 1, Dv BUFSIZ

     Remarks: this macro is sometimes abused to emulate optional arguments for
     commands; the correct macros to use for this purpose are Op, Oo, and Oc.

     See also Bo.

   Brc
     Close a Bro block.  Does not have any tail arguments.

   Bro
     Begin a block enclosed by curly braces.  Does not have any head
     arguments.

     Examples:
           .Bro 1 , ... ,
           .Va n Brc

     See also Brq.

   Brq
     Encloses its arguments in curly braces.

     Examples:
           .Brq 1, ..., Va n

     See also Bro.

   Bsx
     Format the BSD/OS version provided as an argument, or a default value if
     no argument is provided.

     Examples:
           .Bsx 1.0
           .Bsx

     See also At, Bx, Dx, Fx, Nx, and Ox.

   Bt
     Supported only for compatibility, do not use this in new manuals.  Prints
     “is currently in beta test.”

   Bx
     Format the BSD version provided as an argument, or a default value if no
     argument is provided.

     Examples:
           .Bx 4.3 Tahoe
           .Bx 4.4
           .Bx

     See also At, Bsx, Dx, Fx, Nx, and Ox.

   Cd
     Kernel configuration declaration.  This denotes strings accepted by
     config(8).  It is most often used in section 4 manual pages.

     Examples:
           .Cd device le0 at scode?

     Remarks: this macro is commonly abused by using quoted literals to retain
     whitespace and align consecutive Cd declarations.  This practise is
     discouraged.

   Cm
     Command modifiers.  Typically used for fixed strings passed as arguments,
     unless Fl is more appropriate.  Also useful when specifying configuration
     options or keys.

     Examples:
           .Nm mt Fl f Ar device Cm rewind
           .Nm ps Fl o Cm pid , Ns Cm command
           .Nm dd Cm if= Ns Ar file1 Cm of= Ns Ar file2
           .Cm IdentityFile Pa ~/.ssh/id_rsa
           .Cm LogLevel Dv DEBUG

   D1
     One-line indented display.  This is formatted by the default rules and is
     useful for simple indented statements.  It is followed by a newline.

     Examples:
           .D1 Fl abcdefgh

     See also Bd and Dl.

   Db
     This macro is obsolete.  No replacement is needed.  It is ignored by
     mandoc(1) and groff including its arguments.  It was formerly used to
     toggle a debugging mode.

   Dc
     Close a Do block.  Does not have any tail arguments.

   Dd
     Document date for display in the page footer.  This is the mandatory
     first macro of any mdoc manual.  Its syntax is as follows:

           .Dd month day, year

     The month is the full English month name, the day is an optionally zero-
     padded numeral, and the year is the full four-digit year.

     Other arguments are not portable; the mandoc(1) utility handles them as
     follows:
        -   To have the date automatically filled in by the OpenBSD version of
            cvs(1), the special string “$Mdocdate$” can be given as an
            argument.
        -   The traditional, purely numeric man(7) format year–month–day is
            accepted, too.
        -   If a date string cannot be parsed, it is used verbatim.
        -   If no date string is given, the current date is used.

     Examples:
           .Dd $Mdocdate$
           .Dd $Mdocdate: July 21 2007$
           .Dd July 21, 2007

     See also Dt and Os.

   Dl
     One-line indented display.  This is formatted as literal text and is
     useful for commands and invocations.  It is followed by a newline.

     Examples:
           .Dl % mandoc mdoc.7 \(ba less

     See also Ql, Bd -literal, and D1.

   Do
     Begin a block enclosed by double quotes.  Does not have any head
     arguments.

     Examples:
           .Do
           April is the cruellest month
           .Dc
           \(em T.S. Eliot

     See also Dq.

   Dq
     Encloses its arguments in “typographic” double-quotes.

     Examples:
           .Dq April is the cruellest month
           \(em T.S. Eliot

     See also Qq, Sq, and Do.

   Dt
     Document title for display in the page header.  This is the mandatory
     second macro of any mdoc file.  Its syntax is as follows:

           .Dt TITLE section [arch]

     Its arguments are as follows:

       TITLE    The document's title (name), defaulting to “UNTITLED” if
                unspecified.  To achieve a uniform appearance of page header
                lines, it should by convention be all caps.

       section  The manual section.  This may be one of 1 (General Commands),
                2 (System Calls), 3 (Library Functions), 3p (Perl Library), 4
                (Device Drivers), 5 (File Formats), 6 (Games), 7
                (Miscellaneous Information), 8 (System Manager's Manual), or 9
                (Kernel Developer's Manual).  It should correspond to the
                manual's filename suffix and defaults to the empty string if
                unspecified.

       arch     This specifies the machine architecture a manual page applies
                to, where relevant, for example alpha, amd64, i386, or
                sparc64.  The list of valid architectures varies by operating
                system.

     Examples:
           .Dt FOO 1
           .Dt FOO 9 i386

     See also Dd and Os.

   Dv
     Defined variables such as preprocessor constants, constant symbols,
     enumeration values, and so on.

     Examples:
           .Dv NULL
           .Dv BUFSIZ
           .Dv STDOUT_FILENO

     See also Er and Ev for special-purpose constants, Va for variable
     symbols, and Fd for listing preprocessor variable definitions in the
     SYNOPSIS.

   Dx
     Format the DragonFly version provided as an argument, or a default value
     if no argument is provided.

     Examples:
           .Dx 2.4.1
           .Dx

     See also At, Bsx, Bx, Fx, Nx, and Ox.

   Ec
     Close a scope started by Eo.  Its syntax is as follows:

           .Ec [TERM]

     The TERM argument is used as the enclosure tail, for example, specifying
     \(rq will emulate Dc.

   Ed
     End a display context started by Bd.

   Ef
     End a font mode context started by Bf.

   Ek
     End a keep context started by Bk.

   El
     End a list context started by Bl.

     See also Bl and It.

   Em
     Request an italic font.  If the output device does not provide that,
     underline.

     This is most often used for stress emphasis (not to be confused with
     importance, see Sy).  In the rare cases where none of the semantic markup
     macros fit, it can also be used for technical terms and placeholders,
     except that for syntax elements, Sy and Ar are preferred, respectively.

     Examples:
           Selected lines are those
           .Em not
           matching any of the specified patterns.
           Some of the functions use a
           .Em hold space
           to save the pattern space for subsequent retrieval.

     See also Bf, Li, No, and Sy.

   En
     This macro is obsolete.  Use Eo or any of the other enclosure macros.

     It encloses its argument in the delimiters specified by the last Es
     macro.

   Eo
     An arbitrary enclosure.  Its syntax is as follows:

           .Eo [TERM]

     The TERM argument is used as the enclosure head, for example, specifying
     \(lq will emulate Do.

   Er
     Error constants for definitions of the errno libc global variable.  This
     is most often used in section 2 and 3 manual pages.

     Examples:
           .Er EPERM
           .Er ENOENT

     See also Dv for general constants.

   Es
     This macro is obsolete.  Use Eo or any of the other enclosure macros.

     It takes two arguments, defining the delimiters to be used by subsequent
     En macros.

   Ev
     Environmental variables such as those specified in environ(7).

     Examples:
           .Ev DISPLAY
           .Ev PATH

     See also Dv for general constants.

   Ex
     Insert a standard sentence regarding command exit values of 0 on success
     and >0 on failure.  This is most often used in section 1, 6, and 8 manual
     pages.  Its syntax is as follows:

           .Ex -std [utility ...]

     If utility is not specified, the document's name set by Nm is used.
     Multiple utility arguments are treated as separate utilities.

     See also Rv.

   Fa
     Function argument or parameter.  Its syntax is as follows:

           .Fa "[argtype] [argname]" ...

     Each argument may be a name and a type (recommended for the SYNOPSIS
     section), a name alone (for function invocations), or a type alone (for
     function prototypes).  If both a type and a name are given or if the type
     consists of multiple words, all words belonging to the same function
     argument have to be given in a single argument to the Fa macro.

     This macro is also used to specify the field name of a structure.

     Most often, the Fa macro is used in the SYNOPSIS within Fo blocks when
     documenting multi-line function prototypes.  If invoked with multiple
     arguments, the arguments are separated by a comma.  Furthermore, if the
     following macro is another Fa, the last argument will also have a
     trailing comma.

     Examples:
           .Fa "const char *p"
           .Fa "int a" "int b" "int c"
           .Fa "char *" size_t

     See also Fo.

   Fc
     End a function context started by Fo.

   Fd
     Preprocessor directive, in particular for listing it in the SYNOPSIS.
     Historically, it was also used to document include files.  The latter
     usage has been deprecated in favour of In.

     Its syntax is as follows:

           .Fd #directive [argument ...]

     Examples:
           .Fd #define sa_handler __sigaction_u.__sa_handler
           .Fd #define SIO_MAXNFDS
           .Fd #ifdef FS_DEBUG
           .Ft void
           .Fn dbg_open "const char *"
           .Fd #endif

     See also MANUAL STRUCTURE, In, and Dv.

   Fl
     Command-line flag or option.  Used when listing arguments to command-line
     utilities.  Prints a fixed-width hyphen ‘-’ directly followed by each
     argument.  If no arguments are provided, a hyphen is printed followed by
     a space.  If the argument is a macro, a hyphen is prefixed to the
     subsequent macro output.

     Examples:
           .Fl R Op Fl H | L | P
           .Op Fl 1AaCcdFfgHhikLlmnopqRrSsTtux
           .Fl type Cm d Fl name Pa CVS
           .Fl Ar signal_number
           .Fl o Fl

     See also Cm.

   Fn
     A function name.  Its syntax is as follows:

           .Fn [functype] funcname [[argtype] argname]

     Function arguments are surrounded in parenthesis and are delimited by
     commas.  If no arguments are specified, blank parenthesis are output.  In
     the SYNOPSIS section, this macro starts a new output line, and a blank
     line is automatically inserted between function definitions.

     Examples:
           .Fn "int funcname" "int arg0" "int arg1"
           .Fn funcname "int arg0"
           .Fn funcname arg0

           .Ft functype
           .Fn funcname

     When referring to a function documented in another manual page, use Xr
     instead.  See also MANUAL STRUCTURE, Fo, and Ft.

   Fo
     Begin a function block.  This is a multi-line version of Fn.  Its syntax
     is as follows:

           .Fo funcname

     Invocations usually occur in the following context:

           .Ft functype
           .Fo funcname
           .Fa "argtype argname"
           ...
           .Fc

     A Fo scope is closed by Fc.

     See also MANUAL STRUCTURE, Fa, Fc, and Ft.

   Fr
     This macro is obsolete.  No replacement markup is needed.

     It was used to show numerical function return values in an italic font.

   Ft
     A function type.  Its syntax is as follows:

           .Ft functype

     In the SYNOPSIS section, a new output line is started after this macro.

     Examples:
           .Ft int
           .Ft functype
           .Fn funcname

     See also MANUAL STRUCTURE, Fn, and Fo.

   Fx
     Format the FreeBSD version provided as an argument, or a default value if
     no argument is provided.

     Examples:
           .Fx 7.1
           .Fx

     See also At, Bsx, Bx, Dx, Nx, and Ox.

   Hf
     This macro is not implemented in mandoc(1).

     It was used to include the contents of a (header) file literally.  The
     syntax was:

           .Hf filename

   Ic
     Designate an internal or interactive command.  This is similar to Cm but
     used for instructions rather than values.

     Examples:
           .Ic :wq
           .Ic hash
           .Ic alias

     Note that using Bd -literal or D1 is preferred for displaying code; the
     Ic macro is used when referring to specific instructions.

   In
     The name of an include file.  This macro is most often used in section 2,
     3, and 9 manual pages.

     When invoked as the first macro on an input line in the SYNOPSIS section,
     the argument is displayed in angle brackets and preceded by "#include",
     and a blank line is inserted in front if there is a preceding function
     declaration.  In other sections, it only encloses its argument in angle
     brackets and causes no line break.

     Examples:
           .In sys/types.h

     See also MANUAL STRUCTURE.

   It
     A list item.  The syntax of this macro depends on the list type.

     Lists of type -hang, -ohang, -inset, and -diag have the following syntax:

           .It args

     Lists of type -bullet, -dash, -enum, -hyphen and -item have the following
     syntax:

           .It

     with subsequent lines interpreted within the scope of the It until either
     a closing El or another It.

     The -tag list has the following syntax:

           .It [args]

     Subsequent lines are interpreted as with -bullet and family.  The line
     arguments correspond to the list's left-hand side; body arguments
     correspond to the list's contents.

     The -column list is the most complicated.  Its syntax is as follows:

           .It cell [<TAB> cell ...]
           .It cell [Ta cell ...]

     The arguments consist of one or more lines of text and macros
     representing a complete table line.  Cells within the line are delimited
     by tabs or by the special Ta block macro.  The tab cell delimiter may
     only be used within the It line itself; on following lines, only the Ta
     macro can be used to delimit cells, and Ta is only recognised as a macro
     when called by other macros, not as the first macro on a line.

     Note that quoted strings may span tab-delimited cells on an It line.  For
     example,

           .It "col1; <TAB> col2 ;" ;

     will preserve the semicolon whitespace except for the last.

     See also Bl.

   Lb
     Specify a library.  The syntax is as follows:

           .Lb library

     The library parameter may be a system library, such as libz or libpam, in
     which case a small library description is printed next to the linker
     invocation; or a custom library, in which case the library name is
     printed in quotes.  This is most commonly used in the SYNOPSIS section as
     described in MANUAL STRUCTURE.

     Examples:
           .Lb libz
           .Lb libmandoc

   Li
     Denotes text that should be in a literal font mode.  Note that this is a
     presentation term and should not be used for stylistically decorating
     technical terms.

     On terminal output devices, this is often indistinguishable from normal
     text.

     See also Bf, Em, No, and Sy.

   Lk
     Format a hyperlink.  Its syntax is as follows:

           .Lk uri [name]

     Examples:
           .Lk http://bsd.lv "The BSD.lv Project"
           .Lk http://bsd.lv

     See also Mt.

   Lp
     Synonym for Pp.

   Ms
     Display a mathematical symbol.  Its syntax is as follows:

           .Ms symbol

     Examples:
           .Ms sigma
           .Ms aleph

   Mt
     Format a “mailto:” hyperlink.  Its syntax is as follows:

           .Mt address

     Examples:
           .Mt discuss@manpages.bsd.lv
           .An Kristaps Dzonsons Aq Mt kristaps@bsd.lv

   Nd
     A one line description of the manual's content.  This is the mandatory
     last macro of the NAME section and not appropriate for other sections.

     Examples:
           .Nd mdoc language reference
           .Nd format and display UNIX manuals

     The Nd macro technically accepts child macros and terminates with a
     subsequent Sh invocation.  Do not assume this behaviour: some whatis(1)
     database generators are not smart enough to parse more than the line
     arguments and will display macros verbatim.

     See also Nm.

   Nm
     The name of the manual page, or — in particular in section 1, 6, and 8
     pages — of an additional command or feature documented in the manual
     page.  When first invoked, the Nm macro expects a single argument, the
     name of the manual page.  Usually, the first invocation happens in the
     NAME section of the page.  The specified name will be remembered and used
     whenever the macro is called again without arguments later in the page.
     The Nm macro uses Block full-implicit semantics when invoked as the first
     macro on an input line in the SYNOPSIS section; otherwise, it uses
     ordinary In-line semantics.

     Examples:

           .Sh SYNOPSIS
           .Nm cat
           .Op Fl benstuv
           .Op Ar

     In the SYNOPSIS of section 2, 3 and 9 manual pages, use the Fn macro
     rather than Nm to mark up the name of the manual page.

   No
     Normal text.  Closes the scope of any preceding in-line macro.  When used
     after physical formatting macros like Em or Sy, switches back to the
     standard font face and weight.  Can also be used to embed plain text
     strings in macro lines using semantic annotation macros.

     Examples:
           .Em italic , Sy bold , No and roman

           .Sm off
           .Cm :C No / Ar pattern No / Ar replacement No /
           .Sm on

     See also Em, Li, and Sy.

   Ns
     Suppress a space between the output of the preceding macro and the
     following text or macro.  Following invocation, input is interpreted as
     normal text just like after an No macro.

     This has no effect when invoked at the start of a macro line.

     Examples:
           .Ar name Ns = Ns Ar value
           .Cm :M Ns Ar pattern
           .Fl o Ns Ar output

     See also No and Sm.

   Nx
     Format the NetBSD version provided as an argument, or a default value if
     no argument is provided.

     Examples:
           .Nx 5.01
           .Nx

     See also At, Bsx, Bx, Dx, Fx, and Ox.

   Oc
     Close multi-line Oo context.

   Oo
     Multi-line version of Op.

     Examples:
           .Oo
           .Op Fl flag Ns Ar value
           .Oc

   Op
     Optional part of a command line.  Prints the argument(s) in brackets.
     This is most often used in the SYNOPSIS section of section 1 and 8 manual
     pages.

     Examples:
           .Op Fl a Ar b
           .Op Ar a | b

     See also Oo.

   Os
     Operating system version for display in the page footer.  This is the
     mandatory third macro of any mdoc file.  Its syntax is as follows:

           .Os [system [version]]

     The optional system parameter specifies the relevant operating system or
     environment.  It is suggested to leave it unspecified, in which case
     mandoc(1) uses its -Ios argument or, if that isn't specified either,
     sysname and release as returned by uname(3).

     Examples:
           .Os
           .Os KTH/CSC/TCS
           .Os BSD 4.3

     See also Dd and Dt.

   Ot
     This macro is obsolete.  Use Ft instead; with mandoc(1), both have the
     same effect.

     Historical mdoc packages described it as “old function type (FORTRAN)”.

   Ox
     Format the OpenBSD version provided as an argument, or a default value if
     no argument is provided.

     Examples:
           .Ox 4.5
           .Ox

     See also At, Bsx, Bx, Dx, Fx, and Nx.

   Pa
     An absolute or relative file system path, or a file or directory name.
     If an argument is not provided, the character ‘~’ is used as a default.

     Examples:
           .Pa /usr/bin/mandoc
           .Pa /usr/share/man/man7/mdoc.7

     See also Lk.

   Pc
     Close parenthesised context opened by Po.

   Pf
     Removes the space between its argument and the following macro.  Its
     syntax is as follows:

           .Pf prefix macro arguments ...

     This is equivalent to:

           .No \&prefix Ns macro arguments ...

     The prefix argument is not parsed for macro names or delimiters, but used
     verbatim as if it were escaped.

     Examples:
           .Pf $ Ar variable_name
           .Pf . Ar macro_name
           .Pf 0x Ar hex_digits

     See also Ns and Sm.

   Po
     Multi-line version of Pq.

   Pp
     Break a paragraph.  This will assert vertical space between prior and
     subsequent macros and/or text.

     Paragraph breaks are not needed before or after Sh or Ss macros or before
     displays (Bd) or lists (Bl) unless the -compact flag is given.

   Pq
     Parenthesised enclosure.

     See also Po.

   Qc
     Close quoted context opened by Qo.

   Ql
     In-line literal display.  This can for example be used for complete
     command invocations and for multi-word code fragments when more specific
     markup is not appropriate and an indented display is not desired.  While
     mandoc(1) always encloses the arguments in single quotes, other
     formatters usually omit the quotes on non-terminal output devices when
     the arguments have three or more characters.

     See also Dl and Bd -literal.

   Qo
     Multi-line version of Qq.

   Qq
     Encloses its arguments in "typewriter" double-quotes.  Consider using Dq.

     See also Dq, Sq, and Qo.

   Re
     Close an Rs block.  Does not have any tail arguments.

   Rs
     Begin a bibliographic (“reference”) block.  Does not have any head
     arguments.  The block macro may only contain %A, %B, %C, %D, %I, %J, %N,
     %O, %P, %Q, %R, %T, %U, and %V child macros (at least one must be
     specified).

     Examples:
           .Rs
           .%A J. E. Hopcroft
           .%A J. D. Ullman
           .%B Introduction to Automata Theory, Languages, and Computation
           .%I Addison-Wesley
           .%C Reading, Massachusetts
           .%D 1979
           .Re

     If an Rs block is used within a SEE ALSO section, a vertical space is
     asserted before the rendered output, else the block continues on the
     current line.

   Rv
     Insert a standard sentence regarding a function call's return value of 0
     on success and -1 on error, with the errno libc global variable set on
     error.  Its syntax is as follows:

           .Rv -std [function ...]

     If function is not specified, the document's name set by Nm is used.
     Multiple function arguments are treated as separate functions.

     See also Ex.

   Sc
     Close single-quoted context opened by So.

   Sh
     Begin a new section.  For a list of conventional manual sections, see
     MANUAL STRUCTURE.  These sections should be used unless it's absolutely
     necessary that custom sections be used.

     Section names should be unique so that they may be keyed by Sx.  Although
     this macro is parsed, it should not consist of child node or it may not
     be linked with Sx.

     See also Pp, Ss, and Sx.

   Sm
     Switches the spacing mode for output generated from macros.  Its syntax
     is as follows:

           .Sm [on | off]

     By default, spacing is on.  When switched off, no white space is inserted
     between macro arguments and between the output generated from adjacent
     macros, but text lines still get normal spacing between words and
     sentences.

     When called without an argument, the Sm macro toggles the spacing mode.
     Using this is not recommended because it makes the code harder to read.

   So
     Multi-line version of Sq.

   Sq
     Encloses its arguments in ‘typewriter’ single-quotes.

     See also Dq, Qq, and So.

   Ss
     Begin a new subsection.  Unlike with Sh, there is no convention for the
     naming of subsections.  Except DESCRIPTION, the conventional sections
     described in MANUAL STRUCTURE rarely have subsections.

     Sub-section names should be unique so that they may be keyed by Sx.
     Although this macro is parsed, it should not consist of child node or it
     may not be linked with Sx.

     See also Pp, Sh, and Sx.

   St
     Replace an abbreviation for a standard with the full form.  The following
     standards are recognised.  Where multiple lines are given without a blank
     line in between, they all refer to the same standard, and using the first
     form is recommended.

     C language standards

        -ansiC          ANSI X3.159-1989 (“ANSI C89”)
        -ansiC-89       ANSI X3.159-1989 (“ANSI C89”)
        -isoC           ISO/IEC 9899:1990 (“ISO C90”)
        -isoC-90        ISO/IEC 9899:1990 (“ISO C90”)
                        The original C standard.

        -isoC-amd1      ISO/IEC 9899/AMD1:1995 (“ISO C90, Amendment 1”)

        -isoC-tcor1     ISO/IEC 9899/TCOR1:1994 (“ISO C90, Technical
                        Corrigendum 1”)

        -isoC-tcor2     ISO/IEC 9899/TCOR2:1995 (“ISO C90, Technical
                        Corrigendum 2”)

        -isoC-99        ISO/IEC 9899:1999 (“ISO C99”)
                        The second major version of the C language standard.

        -isoC-2011      ISO/IEC 9899:2011 (“ISO C11”)
                        The third major version of the C language standard.

     POSIX.1 before the Single UNIX Specification

        -p1003.1-88     IEEE Std 1003.1-1988 (“POSIX.1”)
        -p1003.1        IEEE Std 1003.1 (“POSIX.1”)
                        The original POSIX standard, based on ANSI C.

        -p1003.1-90     IEEE Std 1003.1-1990 (“POSIX.1”)
        -iso9945-1-90   ISO/IEC 9945-1:1990 (“POSIX.1”)
                        The first update of POSIX.1.

        -p1003.1b-93    IEEE Std 1003.1b-1993 (“POSIX.1b”)
        -p1003.1b       IEEE Std 1003.1b (“POSIX.1b”)
                        Real-time extensions.

        -p1003.1c-95    IEEE Std 1003.1c-1995 (“POSIX.1c”)
                        POSIX thread interfaces.

        -p1003.1i-95    IEEE Std 1003.1i-1995 (“POSIX.1i”)
                        Technical Corrigendum.

        -p1003.1-96     ISO/IEC 9945-1:1996 (“POSIX.1”)
        -iso9945-1-96   ISO/IEC 9945-1:1996 (“POSIX.1”)
                        Includes POSIX.1-1990, 1b, 1c, and 1i.

     X/Open Portability Guide version 4 and related standards

        -xpg3           X/Open Portability Guide Issue 3 (“XPG3”)
                        An XPG4 precursor, published in 1989.

        -p1003.2        IEEE Std 1003.2 (“POSIX.2”)
        -p1003.2-92     IEEE Std 1003.2-1992 (“POSIX.2”)
        -iso9945-2-93   ISO/IEC 9945-2:1993 (“POSIX.2”)
                        An XCU4 precursor.

        -p1003.2a-92    IEEE Std 1003.2a-1992 (“POSIX.2”)
                        Updates to POSIX.2.

        -xpg4           X/Open Portability Guide Issue 4 (“XPG4”)
                        Based on POSIX.1 and POSIX.2, published in 1992.

     Single UNIX Specification version 1 and related standards

        -susv1          Version 1 of the Single UNIX Specification (“SUSv1”)
        -xpg4.2         X/Open Portability Guide Issue 4, Version 2 (“XPG4.2”)
                        This standard was published in 1994.  It was used as
                        the basis for UNIX 95 certification.  The following
                        three refer to parts of it.

        -xsh4.2         X/Open System Interfaces and Headers Issue 4, Version 2
                        (“XSH4.2”)

        -xcurses4.2     X/Open Curses Issue 4, Version 2 (“XCURSES4.2”)

        -p1003.1g-2000  IEEE Std 1003.1g-2000 (“POSIX.1g”)
                        Networking APIs, including sockets.

        -svid4          System V Interface Definition, Fourth Edition
                        (“SVID4”),
                        Published in 1995.

     Single UNIX Specification version 2 and related standards

        -susv2          Version 2 of the Single UNIX Specification (“SUSv2”)
                        This Standard was published in 1997 and is also called
                        X/Open Portability Guide version 5.  It was used as
                        the basis for UNIX 98 certification.  The following
                        refer to parts of it.

        -xbd5           X/Open Base Definitions Issue 5 (“XBD5”)

        -xsh5           X/Open System Interfaces and Headers Issue 5 (“XSH5”)

        -xcu5           X/Open Commands and Utilities Issue 5 (“XCU5”)

        -xns5           X/Open Networking Services Issue 5 (“XNS5”)
        -xns5.2         X/Open Networking Services Issue 5.2 (“XNS5.2”)

     Single UNIX Specification version 3

        -p1003.1-2001  IEEE Std 1003.1-2001 (“POSIX.1”)
        -susv3         Version 3 of the Single UNIX Specification (“SUSv3”)
                       This standard is based on C99, SUSv2, POSIX.1-1996, 1d,
                       and 1j.  It is also called X/Open Portability Guide
                       version 6.  It is used as the basis for UNIX 03
                       certification.

        -p1003.1-2004  IEEE Std 1003.1-2004 (“POSIX.1”)
                       The second and last Technical Corrigendum.

     Single UNIX Specification version 4

        -p1003.1-2008   IEEE Std 1003.1-2008 (“POSIX.1”)
        -susv4          Version 4 of the Single UNIX Specification (“SUSv4”)
                        This standard is also called X/Open Portability Guide
                        version 7.

        -p1003.1-2013   IEEE Std 1003.1-2008/Cor 1-2013 (“POSIX.1”)
                        This is the first Technical Corrigendum.

     Other standards

        -ieee754        IEEE Std 754-1985
                        Floating-point arithmetic.

        -iso8601        ISO 8601
                        Representation of dates and times, published in 1988.

        -iso8802-3      ISO 8802-3: 1989
                        Ethernet local area networks.

        -ieee1275-94    IEEE Std 1275-1994 (“Open Firmware”)

   Sx
     Reference a section or subsection in the same manual page.  The
     referenced section or subsection name must be identical to the enclosed
     argument, including whitespace.

     Examples:
           .Sx MANUAL STRUCTURE

     See also Sh and Ss.

   Sy
     Request a boldface font.

     This is most often used to indicate importance or seriousness (not to be
     confused with stress emphasis, see Em).  When none of the semantic macros
     fit, it is also adequate for syntax elements that have to be given or
     that appear verbatim.

     Examples:
           .Sy Warning :
           If
           .Sy s
           appears in the owner permissions, set-user-ID mode is set.
           This utility replaces the former
           .Sy dumpdir
           program.

     See also Bf, Em, Li, and No.

   Ta
     Table cell separator in Bl -column lists; can only be used below It.

   Tn
     Supported only for compatibility, do not use this in new manuals.  Even
     though the macro name (“tradename”) suggests a semantic function,
     historic usage is inconsistent, mostly using it as a presentation-level
     macro to request a small caps font.

   Ud
     Supported only for compatibility, do not use this in new manuals.  Prints
     out “currently under development.”

   Ux
     Supported only for compatibility, do not use this in new manuals.  Prints
     out “UNIX”.

   Va
     A variable name.

     Examples:
           .Va foo
           .Va const char *bar;

     For function arguments and parameters, use Fa instead.  For declarations
     of global variables in the SYNOPSIS section, use Vt.

   Vt
     A variable type.

     This is also used for indicating global variables in the SYNOPSIS
     section, in which case a variable name is also specified.  Note that it
     accepts Block partial-implicit syntax when invoked as the first macro on
     an input line in the SYNOPSIS section, else it accepts ordinary In-line
     syntax.  In the former case, this macro starts a new output line, and a
     blank line is inserted in front if there is a preceding function
     definition or include directive.

     Examples:
           .Vt unsigned char
           .Vt extern const char * const sys_signame[] ;

     For parameters in function prototypes, use Fa instead, for function
     return types Ft, and for variable names outside the SYNOPSIS section Va,
     even when including a type with the name.  See also MANUAL STRUCTURE.

   Xc
     Close a scope opened by Xo.

   Xo
     Extend the header of an It macro or the body of a partial-implicit block
     macro beyond the end of the input line.  This macro originally existed to
     work around the 9-argument limit of historic roff(7).

   Xr
     Link to another manual ("cross-reference").  Its syntax is as follows:

           .Xr name [section]

     Cross reference the name and section number of another man page; omitting
     the section number is rarely useful.

     Examples:
           .Xr mandoc 1
           .Xr mandoc 1 ;
           .Xr mandoc 1 Ns s behaviour

   br
     Emits a line-break.  This macro should not be used; it is implemented for
     compatibility with historical manuals.

     Consider using Pp in the event of natural paragraph breaks.

   sp
     Emits vertical space.  This macro should not be used; it is implemented
     for compatibility with historical manuals.  Its syntax is as follows:

           .sp [height]

     The height argument is a scaling width as described in roff(7).  If
     unspecified, sp asserts a single vertical space.

MACRO SYNTAX
     The syntax of a macro depends on its classification.  In this section,
     ‘-arg’ refers to macro arguments, which may be followed by zero or more
     ‘parm’ parameters; ‘Yo’ opens the scope of a macro; and if specified,
     ‘Yc’ closes it out.

     The Callable column indicates that the macro may also be called by
     passing its name as an argument to another macro.  For example, ‘.Op Fl O
     Ar file’ produces ‘[-O file]’.  To prevent a macro call and render the
     macro name literally, escape it by prepending a zero-width space, ‘\&’.
     For example, ‘Op \&Fl O’ produces ‘[Fl O]’.  If a macro is not callable
     but its name appears as an argument to another macro, it is interpreted
     as opaque text.  For example, ‘.Fl Sh’ produces ‘-Sh’.

     The Parsed column indicates whether the macro may call other macros by
     receiving their names as arguments.  If a macro is not parsed but the
     name of another macro appears as an argument, it is interpreted as opaque
     text.

     The Scope column, if applicable, describes closure rules.

   Block full-explicit
     Multi-line scope closed by an explicit closing macro.  All macros
     contains bodies; only Bf and (optionally) Bl contain a head.

           .Yo [-arg [parm...]] [head...]
           [body...]
           .Yc

           Macro     Callable     Parsed     Scope
           Bd        No           No         closed by Ed
           Bf        No           No         closed by Ef
           Bk        No           No         closed by Ek
           Bl        No           No         closed by El
           Ed        No           No         opened by Bd
           Ef        No           No         opened by Bf
           Ek        No           No         opened by Bk
           El        No           No         opened by Bl

   Block full-implicit
     Multi-line scope closed by end-of-file or implicitly by another macro.
     All macros have bodies; some (It -bullet, -hyphen, -dash, -enum, -item)
     don't have heads; only one (It in Bl -column) has multiple heads.

           .Yo [-arg [parm...]] [head... [Ta head...]]
           [body...]

           Macro     Callable     Parsed     Scope
           It        No           Yes        closed by It, El
           Nd        No           No         closed by Sh
           Nm        No           Yes        closed by Nm, Sh, Ss
           Sh        No           Yes        closed by Sh
           Ss        No           Yes        closed by Sh, Ss

     Note that the Nm macro is a Block full-implicit macro only when invoked
     as the first macro in a SYNOPSIS section line, else it is In-line.

   Block partial-explicit
     Like block full-explicit, but also with single-line scope.  Each has at
     least a body and, in limited circumstances, a head (Fo, Eo) and/or tail
     (Ec).

           .Yo [-arg [parm...]] [head...]
           [body...]
           .Yc [tail...]

           .Yo [-arg [parm...]] [head...] [body...] Yc [tail...]

           Macro     Callable     Parsed     Scope
           Ac        Yes          Yes        opened by Ao
           Ao        Yes          Yes        closed by Ac
           Bc        Yes          Yes        closed by Bo
           Bo        Yes          Yes        opened by Bc
           Brc       Yes          Yes        opened by Bro
           Bro       Yes          Yes        closed by Brc
           Dc        Yes          Yes        opened by Do
           Do        Yes          Yes        closed by Dc
           Ec        Yes          Yes        opened by Eo
           Eo        Yes          Yes        closed by Ec
           Fc        Yes          Yes        opened by Fo
           Fo        No           No         closed by Fc
           Oc        Yes          Yes        closed by Oo
           Oo        Yes          Yes        opened by Oc
           Pc        Yes          Yes        closed by Po
           Po        Yes          Yes        opened by Pc
           Qc        Yes          Yes        opened by Oo
           Qo        Yes          Yes        closed by Oc
           Re        No           No         opened by Rs
           Rs        No           No         closed by Re
           Sc        Yes          Yes        opened by So
           So        Yes          Yes        closed by Sc
           Xc        Yes          Yes        opened by Xo
           Xo        Yes          Yes        closed by Xc

   Block partial-implicit
     Like block full-implicit, but with single-line scope closed by the end of
     the line.

           .Yo [-arg [val...]] [body...] [res...]

           Macro     Callable     Parsed
           Aq        Yes          Yes
           Bq        Yes          Yes
           Brq       Yes          Yes
           D1        No           Yes
           Dl        No           Yes
           Dq        Yes          Yes
           En        Yes          Yes
           Op        Yes          Yes
           Pq        Yes          Yes
           Ql        Yes          Yes
           Qq        Yes          Yes
           Sq        Yes          Yes
           Vt        Yes          Yes

     Note that the Vt macro is a Block partial-implicit only when invoked as
     the first macro in a SYNOPSIS section line, else it is In-line.

   Special block macro
     The Ta macro can only be used below It in Bl -column lists.  It delimits
     blocks representing table cells; these blocks have bodies, but no heads.

           Macro     Callable     Parsed     Scope
           Ta        Yes          Yes        closed by Ta, It

   In-line
     Closed by the end of the line, fixed argument lengths, and/or subsequent
     macros.  In-line macros have only text children.  If a number (or
     inequality) of arguments is (n), then the macro accepts an arbitrary
     number of arguments.

           .Yo [-arg [val...]] [args...] [res...]

           .Yo [-arg [val...]] [args...] Yc...

           .Yo [-arg [val...]] arg0 arg1 argN

           Macro     Callable     Parsed     Arguments
           %A        No           No         >0
           %B        No           No         >0                                                  
           %C        No           No         >0                                                  
           %D        No           No         >0                                                  
           %I        No           No         >0                                                  
           %J        No           No         >0                                                  
           %N        No           No         >0                                                  
           %O        No           No         >0                                                  
           %P        No           No         >0                                                  
           %Q        No           No         >0                                                  
           %R        No           No         >0                                                  
           %T        No           No         >0                                                  
           %U        No           No         >0                                                  
           %V        No           No         >0
           Ad        Yes          Yes        >0
           An        Yes          Yes        >0
           Ap        Yes          Yes        0
           Ar        Yes          Yes        n
           At        Yes          Yes        1
           Bsx       Yes          Yes        n
           Bt        No           No         0
           Bx        Yes          Yes        n
           Cd        Yes          Yes        >0
           Cm        Yes          Yes        >0
           Db        No           No         1
           Dd        No           No         n
           Dt        No           No         n
           Dv        Yes          Yes        >0
           Dx        Yes          Yes        n
           Em        Yes          Yes        >0
           Er        Yes          Yes        >0
           Es        Yes          Yes        2
           Ev        Yes          Yes        >0
           Ex        No           No         n
           Fa        Yes          Yes        >0
           Fd        No           No         >0
           Fl        Yes          Yes        n
           Fn        Yes          Yes        >0
           Fr        Yes          Yes        >0
           Ft        Yes          Yes        >0
           Fx        Yes          Yes        n
           Hf        No           No         n
           Ic        Yes          Yes        >0
           In        No           No         1
           Lb        No           No         1
           Li        Yes          Yes        >0
           Lk        Yes          Yes        >0
           Lp        No           No         0
           Ms        Yes          Yes        >0
           Mt        Yes          Yes        >0
           Nm        Yes          Yes        n
           No        Yes          Yes        0
           Ns        Yes          Yes        0
           Nx        Yes          Yes        n
           Os        No           No         n
           Ot        Yes          Yes        >0
           Ox        Yes          Yes        n
           Pa        Yes          Yes        n
           Pf        Yes          Yes        1
           Pp        No           No         0
           Rv        No           No         n
           Sm        No           No         <2
           St        No           Yes        1
           Sx        Yes          Yes        >0
           Sy        Yes          Yes        >0
           Tn        Yes          Yes        >0
           Ud        No           No         0
           Ux        Yes          Yes        n
           Va        Yes          Yes        n
           Vt        Yes          Yes        >0
           Xr        Yes          Yes        >0
           br        No           No         0
           sp        No           No         1

   Delimiters
     When a macro argument consists of one single input character considered
     as a delimiter, the argument gets special handling.  This does not apply
     when delimiters appear in arguments containing more than one character.
     Consequently, to prevent special handling and just handle it like any
     other argument, a delimiter can be escaped by prepending a zero-width
     space (‘\&’).  In text lines, delimiters never need escaping, but may be
     used as normal punctuation.

     For many macros, when the leading arguments are opening delimiters, these
     delimiters are put before the macro scope, and when the trailing
     arguments are closing delimiters, these delimiters are put after the
     macro scope.  For example,

           .Aq ( [ word ] ) .

     renders as:

           ([⟨word⟩]).

     Opening delimiters are:

           (       left parenthesis
           [       left bracket

     Closing delimiters are:

           .       period
           ,       comma
           :       colon
           ;       semicolon
           )       right parenthesis
           ]       right bracket
           ?       question mark
           !       exclamation mark

     Note that even a period preceded by a backslash (‘\.’) gets this special
     handling; use ‘\&.’ to prevent that.

     Many in-line macros interrupt their scope when they encounter delimiters,
     and resume their scope when more arguments follow that are not
     delimiters.  For example,

           .Fl a ( b | c \*(Ba d ) e

     renders as:

           -a (-b | -c | -d) -e

     This applies to both opening and closing delimiters, and also to the
     middle delimiter:

           |       vertical bar

     As a special case, the predefined string \*(Ba is handled and rendered in
     the same way as a plain ‘|’ character.  Using this predefined string is
     not recommended in new manuals.

   Font handling
     In mdoc documents, usage of semantic markup is recommended in order to
     have proper fonts automatically selected; only when no fitting semantic
     markup is available, consider falling back to Physical markup macros.
     Whenever any mdoc macro switches the roff(7) font mode, it will
     automatically restore the previous font when exiting its scope.  Manually
     switching the font using the roff(7) ‘\f’ font escape sequences is never
     required.

COMPATIBILITY
     This section provides an incomplete list of compatibility issues between
     mandoc and GNU troff ("groff").

     The following problematic behaviour is found in groff:

     -   Dd with non-standard arguments behaves very strangely.  When there
         are three arguments, they are printed verbatim.  Any other number of
         arguments is replaced by the current date, but without any arguments
         the string “Epoch” is printed.
     -   Lk only accepts a single link-name argument; the remainder is
         misformatted.
     -   Pa does not format its arguments when used in the FILES section under
         certain list types.
     -   Ta can only be called by other macros, but not at the beginning of a
         line.
     -   %C is not implemented (up to and including groff-1.22.2).
     -   ‘\f’ (font face) and ‘\F’ (font family face) Text Decoration escapes
         behave irregularly when specified within line-macro scopes.
     -   Negative scaling units return to prior lines.  Instead, mandoc
         truncates them to zero.

     The following features are unimplemented in mandoc:

     -   Bd -file file is unsupported for security reasons.
     -   Bd -filled does not adjust the right margin, but is an alias for Bd
         -ragged.
     -   Bd -literal does not use a literal font, but is an alias for Bd
         -unfilled.
     -   Bd -offset center and -offset right don't work.  Groff does not
         implement centered and flush-right rendering either, but produces
         large indentations.

SEE ALSO
     man(1), mandoc(1), eqn(7), man(7), mandoc_char(7), roff(7), tbl(7)

HISTORY
     The mdoc language first appeared as a troff macro package in 4.4BSD.  It
     was later significantly updated by Werner Lemberg and Ruslan Ermilov in
     groff-1.17.  The standalone implementation that is part of the mandoc(1)
     utility written by Kristaps Dzonsons appeared in OpenBSD 4.6.

AUTHORS
     The mdoc reference was written by Kristaps Dzonsons <kristaps@bsd.lv>.

FreeBSD 12.0-CURRENT           November 5, 2015           FreeBSD 12.0-CURRENT
