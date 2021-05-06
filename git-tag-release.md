## Tag a new release

```shell
git tag -a 0.0.1-beta -m "Initial beta release"
git push origin --tags
```

## Overwrite a tag

For example, if `goreleaser` fails.

```shell
# Delete the tag on the remote
git push origin :refs/tags/0.0.2-beta

# Overwrite the local tag, note the `-f` flag
git tag -fa 0.0.2-beta -m "Second beta release"

# Update the remote tags
git push origin --tags
```
