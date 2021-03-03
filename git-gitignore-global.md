# Ignore some files in all repositories

There are some things which, IMO, never are stored in a repository unless by mistake.

To create a _global_ ignore file:

```shell
 git config --global core.excludesfile ~/.gitignore_global
```

Content of `~/.gitignore_global`:

```gitignore
.vscode
.idea
```
