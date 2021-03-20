# Change default branch name for `git init`

In Git 2.28 (released 27th July 2020), a new configuration option, `init.defaultBranch` had been introduced to replace the hard-coded term `master` for the initial branch:

```shell
git config --global init.defaultBranch main
```

After setting this variable, running `git init` will produce a new empty repository whose initial branch is named `main`. Jee! :shipit:

More details: [Highlights from Git 2.28 (GitHub Blog)][git]

[git]: https://github.blog/2020-07-27-highlights-from-git-2-28/#introducing-init-defaultbranch
