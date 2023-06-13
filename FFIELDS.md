# FFIELDS

FFIELDS — Reads a file and prints fields in a specified format.

Syntax:\
**FFIELDS** /A:*attribs* /C /CP:*n* /E /F:"*format*" /H /L:*string* /N /P /Q /S /T /W /X *filename…*

| /A:*attribs* | attributes mask; valid flags are -ACEHIORS |
| --- | --- |
| /C | separate fields at commas |
| /CP:*n* | interpret non-Unicode input text using [code page](<TakeCommandConsolePlugins.md#codepages>) *n* |
| /E | separate fields at first unquoted equals sign |
| [/F:"*format*](<TakeCommandConsolePlugins.md#ff\_swf>)" | format string; see below |
| /H | display filenames |
| [/L:*string*](<TakeCommandConsolePlugins.md#ff\_swl>) | insert line numbers on the left |
| [/N](<TakeCommandConsolePlugins.md#ff\_swn>) | disable features |
| /P | page output |
| /Q | remove quotes (the default is to retain them) |
| /S | search in subdirectories for matching files |
| /T | separate fields at tabs |
| /W | separate fields at whitespace |
| [/X](<TakeCommandConsolePlugins.md#ff\_swx>) | perform variable expansion on each line |
| … | [Range options](<TakeCommandConsolePlugins.md#ranges>) are also supported. |


The FFIELDS command reads a file, divides each line into fields (blank lines are skipped), and then prints the fields using a format string. FFIELDS can read from disk files or from a pipe. If you want to pipe to FFIELDS, remember that pipes open a new shell. To pipe to a plugin command, you must either ensure that the plugin is loaded in the transient shell, *e.g.* by installing the .DLL file in the shell’s PLUGINS directory; or else use temporary files or an in-process pipe.

You may specify more than one *filename*; wildcards and directory aliases are supported. You can search recursively into subdirectories for matching files with /S. @File lists and internet files are supported. You may also specify CLIP: to read from the clipboard instead of a file.

The format string may contain $*n* to print field *n*, or $*n*=*wf* to print field *n* truncated to length *w*; the final letter is L to left-justify the field if it contains fewer than *w* characters, R to right-justify it, C to center it, or T to simply truncate the field without padding it to length *w*. For example, a field specifier of $4=10L would print field 4, left-justified to 10 characters. Use $$ to print a literal dollar sign, or $N to insert a line break.

Fields are numbered starting from 0.

&nbsp;

set \|\! ffields /e /f:"$0=20l $1=58t"

…displays variable names truncated to 20 characters, followed by a space and the variables’ values truncated to 58 characters.

If you include /L on the command line, FFIELDS will insert line numbers to the left of each output line. Lines are numbered starting at 0. If you include the optional *string* argument, FFIELDS will perform variable expansion on it before prepending it to each output line; use the variable \_LINE to get the current line number. For example, /L:"%%@FORMAT\[03,%%\_LINE\]" will prepend the line number, zero-padded to at least three digits.

If you don’t specify a *format* string, FFIELDS will invent one at random:

&nbsp;

alias \|\! ffields /e

/N disables features:

| /NB | do not write a Byte Order Mark |
| --- | --- |
| /NC | disable [highlight](<TakeCommandConsolePlugins.md#highlight>) |
| /ND | do not search into hidden directories; only useful with /S |
| /NF | suppress the file-not-found error |
| /NJ | do not search into junctions; only useful with /S |
| /NZ | do not search into system directories; only useful with /S |


You can combine these, *e.g.* /NDJ.

/X does variable expansion on each line before displaying it. You could, for example, count the characters in each alias definition:

&nbsp;

alias \|\! ffields /e /f:"$0 = %%@len\[$1\]" /x

&nbsp;

Source: [TextUtils Plugin (unm.edu)](<http://prospero.unm.edu/plugins/textutils.html#ffields>)


***
_Created with the Personal Edition of HelpNDoc: [Free Kindle producer](<https://www.helpndoc.com/feature-tour/create-ebooks-for-amazon-kindle>)_
