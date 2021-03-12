# Smarter force-pushing in Git

Git’s `push --force` is destructive because it unconditionally overwrites the remote repository with the local content, possibly overwriting any changes that a team member has pushed in the meantime. 

There is a better way; the option `–-force-with-lease` can help when you do need to do a forced push but still ensure you don’t overwrite other’s work.

More information: [Atlassian Developer](https://blog.developer.atlassian.com/force-with-lease/) article.
