# Grep in all Go files

``` Shell
 grep -inr --include \*.go  reflect ./
```

* `-i` ignore case
* `-r` recursive search (descend into subdirectories)
* `-n`  each output line is preceded by its relative line number in the file
* `--include` only files with a specified extension
* `reflect` is the keyword to search for
* `./` where to begin search (current directory)