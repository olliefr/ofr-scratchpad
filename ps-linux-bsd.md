# Get snapshot of current processes

I just found out that all these years I've been using *BSD syntax* to call `ps`. There is also a "standard" syntax. The output is not identical but both give the information that I'm after most of the time...

## "Standard" syntax

```shell
$ ps -ef
```

Where

* `-e` selects all processes
* `-f` shows "extended" information


## BSD syntax

```shell
$ ps aux
```

Where

* `a` lift the BSD-style "only yourself" restriction
* `u` extra information?
* `x` lift the BSD-style "must have a tty" restriction

## Musings

Why? Who knows...