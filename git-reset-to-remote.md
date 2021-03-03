# Reset local branch to remote branch HEAD

First, reset to the previously fetched `HEAD` of the corresponding upstream branch:

```shell
git reset --hard @{u}
```

The advantage of specifying `@{u}` or its verbose form `@{upstream}` is that the name of the remote repo and branch don't have to be explicitly specified. 

Next, as needed, remove untracked files, optionally also with `-x`:

```shell
git clean -df
```

Finally, as needed, get the latest changes:

```shell
git pull
```

Source: [StackOverflow](https://stackoverflow.com/a/28441119)
