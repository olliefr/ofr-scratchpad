# Rebase current branch on `master`

The following command returns the number of commits ahead of `master`. That is, how many commits ahead your active branch is.

```shell
git rev-list --count HEAD ^master
```

Then, rebase using the following command, where `N` is the number from the previous step. This will open up the editor, where you can choose how to handle individual commits (squash/drop/fixup/etc) and also to edit the commit message. This way all previous commit messages can be organised into the final commit message.

```shell
git rebase -i HEAD~N
```

If, for whatever reason, you want to cancel rebasing and go back, use `git rebase --abort` before the rebase is made.

That's it!
