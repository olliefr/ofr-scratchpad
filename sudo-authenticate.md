# Make `sudo` stop asking for a password

When I run [Ubuntu Linux](https://ubuntu.com/) under [WSL](https://docs.microsoft.com/en-gb/windows/wsl/) on my desktop, I do not want to input `sudo` password when I require elevated user access rights. I still would like to use `sudo` though to separate user and admin level activities.

## Procedure

Instead of amending the default `sudo` configuration in `/etc/sudoers`, I create a new file containing only overrides. My login, naturally, is `ofr`.

First, make an empty file.

```Shell
$ sudo touch /etc/sudoers.d/10-ofr
```

Then, populate it with the overrides.

```
# This is /etc/sudoers.d/10-ofr
# Do not lecture me or ask for a password when using sudo

Defaults:ofr    !lecture
Defaults:ofr    !authenticate
```

Set strict permissions on the overrides file. The permissions match those of an example file in the same directory.

```Shell
$ sudo chmod 440 /etc/sudoers.d/10-ofr
```

## Test

```Shell
# Clear cached password, in case there was any
$ sudo -k

# Run a command which requires elevated access rights
$ sudo apt update
```

It worked!

## More Information

I found `sudoers(7)` rather dry and unhelpful, apart from the *Examples* section.

&mdash; Oliver Frolovs, 2020