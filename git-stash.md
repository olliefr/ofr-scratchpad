# Move uncomitted changes between Git branches

Sometimes I start working on a *wrong branch* of the project. But uncommitted changes can be moved.

* *Stage* changes to the *working tree*
  ```Shell
  $ git add .
  ```
* *Stash* the contents of the *staging area*
  ```Shell
  $ git stash
  ```
* Then checkout the *correct* branch
  ```Shell
  $ git checkout master
  ```
* Remove a single *stashed* state from the *stash list* and apply it on top of the current *working tree* state
  ```Shell
  $ git stash pop
  ```
* Verify that the state has been moved and the *stash list* is empty
  ```Shell
  $ git stash list
  ```
  
* Proceed as usual &ndash; edit, stage, commit to the correct branch.

&mdash; Oliver Frolovs, 2020