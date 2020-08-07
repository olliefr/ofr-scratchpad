# SSH copy and complex file names (`scp`)

When copying a file with a somewhat complex file name (spaces, parentheses) using `scp`, the file name must be enclosed in quotes *twice*: 

```
"'Frolovs, Oliver — Hello Gruffalo (Virgin_Tear_ Lake City Publishing 2020).pdf'"
```

The `scp` is invoked:

```Shell
$ scp -i CERT.pem USER@DOMAIN:"'Horses, Obvs - Why Not (2007 _).pdf'"
```

This, however, might fail for *some* file names, resulting in a cryptic error message displayed:

```
protocol error: filename does not match request
```

Without going into much detail, the way to disable the check that results in this message, is to use `-T` parameter:

```Shell
$ scp -T -i CERT.pem USER@DOMAIN:"'Horses, Obvs - Why Not (2007 _).pdf'"
```

Because, why not? Obviously.

&mdash; Oliver Frolovs, 2020