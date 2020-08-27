# Allow Unrelated Histories to Merge in Git

When I add a new repository to GitHub, I like to initialise it with a README file and a License. This creates a problem later if this (still "empty") repository is later set as an upstream repository for some local repository containing data.

The trick is to allow unrelated histories to merge when pulling the remote.

```Shell
# Add GitHub repo as a remote origin/master
# (DONE)

# Set origin/master as an upstream repo
git branch --set-upstream-to=origin/master master

# Pull from the remote
git pull --allow-unrelated-histories

# Push the results of the merge back to GitHub
$git push origin master
```

That's it.