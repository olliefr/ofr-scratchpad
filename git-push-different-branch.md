# Push local branch to remote in Git 

To publish a local branch *under a different name* in a remote Git repo.

```shell
$ git push <REMOTE> <LOCAL_BRANCH>:<REMOTE_BRANCH>
```

## Example

```shell
$ git push origin rest-importer:wip/rest-importer
```
