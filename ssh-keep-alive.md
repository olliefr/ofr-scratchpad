# Keep SSH session alive

This note is about the [OpenSSH](https://www.openssh.com/) client.

The parameter `ServerAliveInterval` can be specified on the command line. If there is no activity for given number of seconds, the client sends a packet to the server to keep the connection open.

```Shell
$ ssh ... -o ServerAliveInterval=60 ... ...@...
```

## Persistence

To apply the keep-alive setting to *all* SSH client connections, put the parameter into the per-user configuration file `~/.ssh/config`. This file is used by the SSH client. Note, that by default the SSH configuration file may not exist.

```
Host *
  ServerAliveInterval 60
```

Because of the potential for abuse, this file must have strict permissions: read/write for the user, and not writable by others. I keep mine to myself.

```Shell
$ chmod 600 ~/.ssh/config
```

## More information

See `ssh_config(5)`.

&mdash; Oliver Frolovs, 2020