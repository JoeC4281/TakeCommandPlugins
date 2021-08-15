@SIFT — Returns the full name of the single largest (smallest, etc.) matching file.

[SIFT Plugin for Take Command](http://prospero.unm.edu/plugins/sift.html)

Syntax:
**%@SIFT**[*filespec,criterion,attribs,flags,stamp*]
```dos
criterion   L, S, O, or N for largest, smallest, oldest, newest; defaults to L
attribs     supported attributes are -ACEHIORS
flags       bitmapped: 1 recurse, 2 no junctions, 4 no hidden directories, 128 exclude Descript.ion files
stamp       A, C, or W for last access, creation, or last write; defaults to W
```
The @SIFT function provides an easy way to find the single largest, smallest, oldest, or newest matching file in a directory or directory tree, without the overhead of an array. It returns a fully-qualified filename. (It only returns a filename; if you want to get the size or time stamps of the file, call TCC’s internal @FILEDATE, @FILESIZE, and @FILETIME functions as usual. This function is potentially very slow, so calling it multiple times to retrieve different information about the same file would be a bad plan.)

You must supply a *filespec*; it may include a directory alias.

If no matching files are found, this function returns an empty string.

**• Note:** While this particular function does not use an array, you still cannot load this plugin in TCC/LE or in older shells which don’t support arrays.
