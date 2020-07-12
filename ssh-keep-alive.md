# Keep SSH session alive

The parameter `ServerAliveInterval` value in seconds can be specified in the SSH config file or on the command line.

```Shell
$ ssh ... -o ServerAliveInterval=60 ... ...@...
```

&mdash; Oliver Frolovs, 2020