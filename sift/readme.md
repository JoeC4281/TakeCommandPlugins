SIFT — Returns a sorted list of files in an array.

Syntax:
```dos
SIFT /A:attribs /C:sep /I /R /T:stamp /U /V /Z n criterion array filespec…
/A:attribs	select files by attributes (the default is all files):
 	      A - not Archived
 	      C - Compressed
 	      E - Encrypted
 	      H - Hidden
 	      I - not Indexed
 	      O - Offline
 	      R - Read-only
 	      S - System
 	      - - a hyphen inverts attributes which follow
/C:sep	Character separating the time from the date
/I	return date stamps in ISO 8601 format, YYYY-MM-DD
/R	recurse into subdirectories
/T:stamp	selects which date stamp to use:
 	      A - last Access
 	      C - Creation
 	      W - last Write (the default)
/U	return date stamps as UTC (not localized)
/V	dump the array to stdout when done
/Z	localize date stamps dumbly, like DIR and Explorer
n	the number of files to return, 1 — 4096; defaults to 10
criterion	the quality used to find and sort files:
 	      /L or LARGEST — find the largest n files (the default)
 	      /S or SMALLEST — find the smallest n files
 	      /O or OLDEST — find the oldest n files
 	      /N or NEWEST — find the newest n files
array	name of the array to create and fill
filespec…	wildcard filespecs to match
 	 
/F	return fully qualified filenames
/NC	do not insert commas in file sizes
/ND	do not recurse into hidden directories; only useful with /R
/NI	do not include Descript.ion files
/NJ	do not recurse into junctions; only useful with /R
```

*filespecs* may use directory aliases, wildcards including character sets in square brackets, and include lists. If you do not specify any *filespec*, then * (all files in the current directory) will be supplied by default.

An *n*-by-3 array will be created to hold the resulting list. (If an array by the same name already exists, that array will be lost.) Column 0 of the array holds filenames, column 1 holds the files’ sizes, and column 2 holds their date stamps. The filenames returned in column 0 will be fully qualified if either /F or /R was specified, or if more than one filespec was supplied; otherwise filenames are stored without paths. The date stamp selected by /T: is returned in column 2, and is also used for sorting if OLDEST or NEWEST is specified.

If LARGEST is specified or there is no criterion, files will be stored in the array in decreasing order of size, i.e. row 0 will hold the largest file, row 1 will hold the next-largest, and so on. If SMALLEST is specified, then files will be stored in increasing order by size. If OLDEST is used, then files will be sorted into chronological order; and NEWEST, in reverse chronological order. If multiple files have the same size or the same date stamp, then the first one discovered “wins” — which one is found first depends on the filesystem.

sift 20 largest bigdlls c:\windows\system32\*.dll

… finds the 20 largest .DLL files in C:\Windows\System32, and sorts them into a 20-by-3 array named BIGDLLS.

Only the *array* name is mandatory:

sift big

… is legal, and will sort the 10 largest files in the current directory into a 10-by-3 array named BIG.
