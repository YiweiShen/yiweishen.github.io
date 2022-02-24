title: glob Module
date: 2017-04-10 00:27:20
tags: python
---
Docs first:
https://docs.python.org/3/library/glob.html
```python
import glob
glob.glob('./[0-9].*') # ['./1.gif', './2.txt']
```
The glob module finds all the pathnames matching a specified pattern according to the rules used by the Unix shell, although results are returned in arbitrary order. 

glob.glob(pathname, *, recursive=False)

Return a possibly-empty list of path names that match pathname, which must be a string containing a path specification. pathname can be either absolute (like /usr/src/Python-1.5/Makefile) or relative (like ../../Tools/*/*.gif), and can contain shell-style wildcards. Broken symlinks are included in the results (as in the shell).

If recursive is true, the pattern “**” will match any files and zero or more directories and subdirectories. If the pattern is followed by an os.sep, only directories and subdirectories match.