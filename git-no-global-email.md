# Force Git to set e-mail address in working copy

It may be my personal quirk, but I really dislike that Git pulls an email address from global config unless you override it on per-repo basis. Or worse, makes up an email address from `whoami` or whatever. I just learned that there is a config option to make it stop doing this.

```shell
git config --global --unset user.email
git config --global user.useConfigOnly true
```

Now email addresses _have to_ be set on a per-repo basis.

Source: [StackOverflow](https://stackoverflow.com/a/49671582)
