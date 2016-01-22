# Introduction #

Documentation is self contained in the program (which is a shell script).  Run it without arguments for help.

An excerpt of the documentation contained in the program is reproduced here:


---



To display help and formatting options:

ascii2gdocs             displays this message<br>

ascii2gdocs -h          displays detailed help<br>

ascii2gdocs -F          displays formatting options<br>



To add files:  use the -a option<br>
<br>
ascii2gdocs -a file<br>
ascii2gdocs -a -<br>



To add files to folders:  separate folder names with | symbol<br>
<br>
ascii2gdocs -a "folder|names|go|here" file<br>
ascii2gdocs -a "folder|names|go|here" -<br>
<br>
<br>
<br>
To update files:  use the -u option<br>
<br>
ascii2gdocs -u file<br>
ascii2gdocs -u -<br>



To add files using a nondefault style:  use the -F # option<br>
<br>
ascii2gdocs -F # -a file<br>
ascii2gdocs -F # -a -<br>

ascii2gdocs -F # -a "folder|names|go|here" file<br>
ascii2gdocs -F # -a "folder|names|go|here" -<br>



To update files using a nondefault style:  use the -F # option<br>
<br>
ascii2gdocs -F # -u file<br>
ascii2gdocs -F # -u -<br>


To perform bulk operations:  use the - option  (see above and examples)<br>
<br>
Specifying - instead of a file name means to receive local file names from<br>
standard input.  Specify one filename or path ending with a filename per line.<br>
See examples.<br>
<br>
<br>
<br>
TIP:  Create a Google Docs folder named "ascii".  When adding ascii files using<br>
this program, always tag them as belonging in the "ascii" folder (plus whatever<br>
additional folders you wish to put them in).  This gives a way to identify all<br>
ascii documents when exporting (backing up) Google Docs.<br>
<br>
<br>
<br>
<blockquote><hr /></blockquote>




Examples:<br>
<br>
EXAMPLE 1:<br>
<br>
To add local file ".bash_profile" to the root folder in Google Docs<br>
(i.e. no folder) with default style:<br>
<br>
ascii2gdocs -a ~/.bash_profile<br>
<br>
or (equivalent)<br>
<br>
ascii2gdocs -a "folder:root" ~/.bash_profile<br>
<br>
<br>
<br>
EXAMPLE 2:<br>
<br>
To add local file ".bash_profile" to folders named "ascii", "config", and<br>
"hostname-foo" with default style:<br>
<br>
ascii2gdocs -a "ascii|config|hostname-foo" ~/.bash_profile<br>
<br>
<br>
<br>
Example 3:<br>
<br>
To add local file ".bash_profile" to a folder named ascii using the style<br>
specified with numeral 2:<br>
<br>
ascii2gdocs -F 2 -a "ascii" ~/.bash_profile<br>
<br>
<br>
<br>
EXAMPLE 4:<br>
<br>
To update ".bash_profile" to Google Docs using default style:<br>
<br>
ascii2gdocs -u ~/.bash_profile<br>
<br>
<br>
<br>
EXAMPLE 5:<br>
<br>
To add all .sh files (shell scripts) under your home directory to folders<br>
named "ascii" and "shell scripts" using the default style:<br>
<br>
find ~ -name '<code>*</code>.sh' -print | ascii2gdocs -a "ascii|shell scripts" -<br>
<br>
<hr />


Google Docs in this documentation means the same as Google Drive.<br>
<br>
This program is intended to enable <code>*</code>NIX/OSX command line users to<br>
programmatically add or update ascii files to Google Docs.  Local ascii files<br>
are converted into Google documents, where they can be edited from a browser,<br>
shared online, worked on collaboratively, have comments and revision histories,<br>
are readily accessible from mobile devices, and do not use up Google Docs quota<br>
space.  Formatting of the Google documents can be specified, such as font, font<br>
size, page size, orienation, borders, text color, and other basic formatting.<br>
Local ascii files can be added or updated one at a time, or in batch.  Files<br>
can be added to one or more folders, or no folders (Google Docs "root").<br>
<br>
Google documents created with this program are given a title in Google Docs.<br>
The title is always identical to the local (base) file name- a different title<br>
can not be specified (unless changed later by other means, for example in the<br>
web interface).<br>
<br>
Any local file can be tried- ascii or not- and there is no requirement that<br>
local files have any particular suffix.  Only file size and number of<br>
characters are checked, to make sure users do not attempt to add or update a<br>
local file that Google Docs will reject, since Google limits conversion of<br>
files to Google Docs to certain maximums.  (2 MB at the time of this writing.)<br>
<br>
Add always creates a new Google document that did not exist before.<br>
<br>
Update never creates a new Google document.<br>
<br>
A log file records the time (YYYYMMDDHHMMSS) of adding or updating, the Google Document's<br>
ID, and the full path to the local file.  (Optionally, the user can disable<br>
logging updates- see program source.)<br>
<br>
There is no output on the command line if there are no errors.  The user can<br>
watch Google Docs or tail -f the log file to monitor progress.<br>
<br>
Various parameters (including default formatting) can be changed by the user by<br>
simply changing the values of variables in the source for this program (a<br>
Bourne shell script).<br>
<br>
This progam is intended to be highly portable among different <code>*</code>NIX platforms,<br>
with minimal dependencies (the only requirement is https enabled cURL version<br>
7.18.0 or higher).  It consists of a single file (shell script) that contains<br>
its own documentation.<br>
<br>
Multiple Google Docs accounts can be used but the user will need to use one<br>
authorization directory per account.  It is left to the user to implement a solution,<br>
different types of solutions are possible (eg. wrapper scripts).<br>
<br>
Usually, one adds a local ascii file to Google Documents only once with this<br>
program.  Subsequentally, if the local ascii file changes and the corresponding<br>
Google Document does not change, update Google Docs with the changes using this<br>
program.  The update will be reflected in the revision history of the<br>
corresponding Google Document (revision history is visible in a browser).<br>
<br>
See basic useage information, users can add documents in bulk by passing in<br>
files to standard input.  This allows for batch jobs that populate many<br>
documents, including initial migration of local files to Google Docs ("moving<br>
to the cloud").<br>
<br>
As its name suggests, this program is not designed to be a two way<br>
syncronization program between Google Documents and local ascii files.