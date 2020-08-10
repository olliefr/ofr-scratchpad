# Open Windows Explorer from WSL Linux shell

 Launch _Windows Explorer_ from a *WSL* shell:

```Shell
$ explorer.exe .
```

## Caveat

The above trick will not work, if Windows interop is turned off in WSL via `/etc/wsl.conf`:

```
# Do not support launching Windows processes
# Do not add Windows PATH to the $PATH variable

[interop]
enabled = false
appendWindowsPath = false
```

&mdash; Oliver Frolovs, 2020