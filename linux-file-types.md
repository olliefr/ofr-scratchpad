# File types in Linux

Note the first letter of the output:

* Block device

  ```shell
  $ ls -l /dev/sda
  brw------- 1 root root 8, 0 Nov 12 02:33 /dev/sda
  ```
* Symbolic link

  ```shell
  $ ls -l /lib
  lrwxrwxrwx 1 root root  7 Apr 23  2020 /lib -> usr/lib
  ```
  
* Hard link

  ```shell
  $ ln /home/ofr/go_dev.md /tmp/go_dev.md
  
  $ ls -l /home/ofr/go_dev.md
  -rw-r--r-- 2 ofr ofr 3998 Oct  8 16:02 /home/ofr/go_dev.md
  
  $ ls -l /tmp/go_dev.md
  -rw-r--r-- 2 ofr ofr 3998 Oct  8 16:02 /tmp/go_dev.md
  
  $ stat --printf '%h\n' /home/ofr/go_dev.md
  2
  
  $ rm /tmp/go_dev.md
  
  $ stat --printf '%h\n' /home/ofr/go_dev.md
  1
  ```
  
* Ordinary file

  ```shell
  $ ls -l /home/ofr/go_dev.md
  -rw-r--r-- 1 ofr ofr 3998 Oct  8 16:02 /home/ofr/go_dev.md
  ```
  
* Directory

  ```shell
  $ ls -l -d /usr/lib
  drwxr-xr-x 84 root root 4096 Nov  4 17:31 /usr/lib
  ```

## What type a file is?

```shell
$ file /dev/sda
```
Or
```shell
$ ls -l .
```

Or
```shell
$ stat [OPTION]... FILE...
```
