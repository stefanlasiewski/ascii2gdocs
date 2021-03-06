# ascii2gdocs

(NOTE: This is an old project created by a former colleague which uses an older version of the Google API. In 2015, I migrated this from Google Code to Github for posterity.)

Enables *NIX/OSX command line users to add or update ascii files to Google Docs. Local ascii files are converted into Google documents, where they can be edited from a browser, shared online, worked on collaboratively, have comments and revision histories, are readily accessible from mobile devices, and do not use up Google Docs quota space. Formatting of the Google documents can be specified, such as font, font size, page size, orienation, borders, text color, and other basic formatting. Local ascii files can be added or updated one at a time, or in batch. Files can be added to one or more folders, or no folders (Google Docs "root").

Original author: Trever Nightingale at Lawrence Berkeley National Laboratory.

Migrated from http://code.google.com/p/ascii2gdocs

#summary Documentation

= Introduction =

Documentation is self contained in the program (which is a shell script).  Run it without arguments for help.

An excerpt of the documentation contained in the program is reproduced here:

----


To display help and formatting options:

    ascii2gdocs             displays this message
    ascii2gdocs -h          displays detailed help
    ascii2gdocs -F          displays formatting options

To add files:  use the -a option

    ascii2gdocs -a file
    ascii2gdocs -a -

To add files to folders:  separate folder names with | symbol

    ascii2gdocs -a "folder|names|go|here" file
    ascii2gdocs -a "folder|names|go|here" -

To update files:  use the -u option

    ascii2gdocs -u file
    ascii2gdocs -u -

To add files using a nondefault style:  use the -F # option

    ascii2gdocs -F # -a file
    ascii2gdocs -F # -a -

    ascii2gdocs -F # -a "folder|names|go|here" file
    ascii2gdocs -F # -a "folder|names|go|here" -

To update files using a nondefault style:  use the -F # option

    ascii2gdocs -F # -u file
    ascii2gdocs -F # -u -


To perform bulk operations:  use the - option  (see above and examples)

Specifying - instead of a file name means to receive local file names from
standard input.  Specify one filename or path ending with a filename per line.
See examples.

TIP:  Create a Google Docs folder named "ascii".  When adding ascii files using
this program, always tag them as belonging in the "ascii" folder (plus whatever
additional folders you wish to put them in).  This gives a way to identify all
ascii documents when exporting (backing up) Google Docs.

----

Examples:

EXAMPLE 1:

To add local file ".bash_profile" to the root folder in Google Docs 
(i.e. no folder) with default style:

    ascii2gdocs -a ~/.bash_profile

or (equivalent)

    ascii2gdocs -a "folder:root" ~/.bash_profile

EXAMPLE 2:

To add local file ".bash_profile" to folders named "ascii", "config", and
"hostname-foo" with default style:

    ascii2gdocs -a "ascii|config|hostname-foo" ~/.bash_profile

Example 3:

To add local file ".bash_profile" to a folder named ascii using the style 
specified with numeral 2:

    ascii2gdocs -F 2 -a "ascii" ~/.bash_profile

EXAMPLE 4:

To update ".bash_profile" to Google Docs using default style:

    ascii2gdocs -u ~/.bash_profile

EXAMPLE 5:

To add all .sh files (shell scripts) under your home directory to folders 
named "ascii" and "shell scripts" using the default style:

    find ~ -name '{{{*}}}.sh' -print | ascii2gdocs -a "ascii|shell scripts" -

----


Google Docs in this documentation means the same as Google Drive.

This program is intended to enable {{{*}}}NIX/OSX command line users to
programmatically add or update ascii files to Google Docs.  Local ascii files
are converted into Google documents, where they can be edited from a browser,
shared online, worked on collaboratively, have comments and revision histories,
are readily accessible from mobile devices, and do not use up Google Docs quota
space.  Formatting of the Google documents can be specified, such as font, font
size, page size, orienation, borders, text color, and other basic formatting.
Local ascii files can be added or updated one at a time, or in batch.  Files
can be added to one or more folders, or no folders (Google Docs "root").

Google documents created with this program are given a title in Google Docs.
The title is always identical to the local (base) file name- a different title
can not be specified (unless changed later by other means, for example in the
web interface).

Any local file can be tried- ascii or not- and there is no requirement that
local files have any particular suffix.  Only file size and number of
characters are checked, to make sure users do not attempt to add or update a
local file that Google Docs will reject, since Google limits conversion of
files to Google Docs to certain maximums.  (2 MB at the time of this writing.)

Add always creates a new Google document that did not exist before.  

Update never creates a new Google document.

A log file records the time (YYYYMMDDHHMMSS) of adding or updating, the Google Document's
ID, and the full path to the local file.  (Optionally, the user can disable
logging updates- see program source.)

There is no output on the command line if there are no errors.  The user can
watch Google Docs or tail -f the log file to monitor progress.

Various parameters (including default formatting) can be changed by the user by
simply changing the values of variables in the source for this program (a
Bourne shell script).

This progam is intended to be highly portable among different {{{*}}}NIX platforms,
with minimal dependencies (the only requirement is https enabled cURL version
7.18.0 or higher).  It consists of a single file (shell script) that contains
its own documentation.

Multiple Google Docs accounts can be used but the user will need to use one 
authorization directory per account.  It is left to the user to implement a solution, 
different types of solutions are possible (eg. wrapper scripts).

Usually, one adds a local ascii file to Google Documents only once with this
program.  Subsequentally, if the local ascii file changes and the corresponding
Google Document does not change, update Google Docs with the changes using this
program.  The update will be reflected in the revision history of the
corresponding Google Document (revision history is visible in a browser).

See basic useage information, users can add documents in bulk by passing in
files to standard input.  This allows for batch jobs that populate many
documents, including initial migration of local files to Google Docs ("moving
to the cloud").

As its name suggests, this program is not designed to be a two way
syncronization program between Google Documents and local ascii files.
