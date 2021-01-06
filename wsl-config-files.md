# WSL configuration

I had a problem with DNS resolving in my **Ubuntu** running under WSL when Mullvad VPN was active. Somehow, WSL did not pick up the changes to DNS configuration from Windows, and the VPN would block access to the "default" DNS servers.

Since I don't require traffic from WSL to go through the VPN, especially so for DNS queries, I dug into WSL configuration looking for information on how to set up the DNS manually.

The top paragraph in the following configuration file disables auto-generation of `resolv.conf` file. Then, I created a static `resolv.conf` file as described in the next section.

My `/etc/wsl.conf`:

```
# Make WSL work under Mullvad VPN
[network]
generateResolvConf = false

# Do not support launching Windows processes
# Do not add Windows PATH to the $PATH variable
[interop]
enabled = false
appendWindowsPath = false
```

The `interop` part is not related to DNS. It is to turn off running Windows applications from WSL. I keep the environments separate so this is best for my needs.

## DNS configuration

Once I set `generateResolvConf = false` in `/etc/wsl.conf` and restarted WSL with

```
C:\ PS> wsl.exe --shutdown
```

I created a static configuration for DNS, pointing to Cloudflare:

**UPDATE** It seems that now `/etc/resolv.conf` is a symlink for `../run/resolvconf/resolv.conf`.
```shell
$ sudo rm /etc/resolv.conf
$ sudo cat > /etc/resolv.conf
# Resolve using Cloudflare DNS, ignoring
# VPN settings in Windows
nameserver 1.1.1.1
nameserver 1.0.0.1
<Ctrl+D>
```

It used to be the case, that:

```shell
$ sudo mv /etc/resolv.conf /etc/resolv.conf.old
$ sudo cat > /etc/resolv.conf
nameserver 1.1.1.1
nameserver 1.0.0.1
<Ctrl+D>
```

And restarted the WSL again. Now I have DNS working in WSL even when my Windows host is connected to VPN and is using the VPN provider's DNS servers. I am happy with the WSL using Cloudflare for DNS.

&mdash; Oliver Frolovs, 2020
