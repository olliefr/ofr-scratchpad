# Git workflows

## GitHub flow

[GitHub Flow](https://guides.github.com/introduction/flow/) appears to be well-suited for asynchronous, exploratory way of working.

* There is only **one** `main` branch. 
* Anything in the `main` branch is always deployable.
* All other branches are whatever but they are *always* based off `main`.

## GitFlow

[GitFlow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) is ideally suited for large projects that have a scheduled release cycle.

* There are `main`, `dev`, and many feature branches.
* Feature branches use `dev` as a parent.
* Feature branches never interact with `main` directly.
* There can be `hotfix` and `release` branches.

