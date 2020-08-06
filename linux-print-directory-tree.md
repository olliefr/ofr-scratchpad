# Print Directory Tree in Linux

I keep forgetting about the `tree` utility!

This is how it works:

```Shell
$ tree /etc

/etc
├── NetworkManager
│   └── dispatcher.d
│       ├── hook-network-manager
│       └── ntp
├── X11
│   ├── Xsession.d
│   │   └── 90gpg-agent
│   └── xkb
├── acpi
│   ├── actions
│   │   ├── hibinit-power.sh
│   │   └── sleep.sh
│   └── events
│       ├── hibinit-power
│       └── hibinit-sleep
├── adduser.conf
├── alternatives
│   ├── README
│   ├── awk -> /usr/bin/gawk
│   ├── awk.1.gz -> /usr/share/man/man1/gawk.1.gz
│   ├── builtins.7.gz -> /usr/share/man/man7/bash-builtins.7.gz
│   ├── editor -> /bin/nano
│   ├── editor.1.gz -> /usr/share/man/man1/nano.1.gz
│   ├── ex -> /usr/bin/vim.basic
[OUTPUT OMITTED]
```

I found it very useful for understanding how various open-source project repositories are organised.

&mdash; Oliver Frolovs, 2020