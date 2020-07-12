# Git Submodules

When a project stored in `Git` depends on another project stored in `Git`.

## Example

The *current working directory* for this example is set to [RTC embedded OS](https://github.com/dawbarton/rtc) repository on my machine:

```Shell
olliefr@GREY-TOWER MINGW64 /c/Local/rtc (master)
```

The [RTC embedded OS](https://github.com/dawbarton/rtc) is built on [TI StarterWare no-OS platform support package](https://github.com/dawbarton/starterware). The package is unlikely to change a lot, so the *workflow for a third party library* from `gitsubmodules(7)` documentation is followed.

```Shell
$ git submodule add https://github.com/olliefr/starterware starterware
```

```
The following paths are ignored by one of your .gitignore files:
starterware
hint: Use -f if you really want to add them.
hint: Turn this message off by running
hint: "git config advice.addIgnoredFile false"
```

Oops, it appears that the destination folder was previously placed on the ignore list, probably to cope with it containing another `Git` repository. Remove it from the `.gitignore` list for the project. The project now looks like the following.

```Shell
$ git diff
```

```
diff --git a/.gitignore b/.gitignore
index f39898a..6ae2fd4 100644
--- a/.gitignore
+++ b/.gitignore
@@ -36,8 +36,5 @@ binary/*
 # Data files
 *.mat

-# Starterware
-starterware
-
 # Matlab temporary files for rig interfaces
 rigs/**/*.asv
```

Try again to include the platform files repository as a `Git` submodule.

```Shell
$ git submodule add https://github.com/olliefr/starterware starterware
```

```
Cloning into 'C:/Local/rtc/starterware'...
remote: Enumerating objects: 1747, done.
remote: Total 1747 (delta 0), reused 0 (delta 0), pack-reused 1747 eceiving objects:  97% (1695/1
Receiving objects: 100% (1747/1747), 10.74 MiB | 7.20 MiB/s, done.
Resolving deltas: 100% (623/623), done.
```

Check the outcome.

```Shell
$ git status
```

```
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   .gitmodules
        new file:   starterware

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   .gitignore
```

**Success!!!** Note, that `.gitmodules` is version-controlled with your other files, like your `.gitignore` file. It’s pushed and pulled with the rest of your project. This is how other people who clone this project know where to get the submodule projects from.

Prepare the commit.

```Shell
$ git add .gitignore
```

```Shell
$ git status
```

```
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   .gitignore
        new file:   .gitmodules
        new file:   starterware
```

Commit and push.

```Shell
$ git commit -m "Adds a Git submodule for TI StarterWare platform support package"
```

```
[master 07e93a6] Adds a Git submodule for TI StarterWare platform support package
 3 files changed, 4 insertions(+), 3 deletions(-)
 create mode 100644 .gitmodules
 create mode 160000 starterware
```

```Shell
$ git push
```

```
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 12 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 514 bytes | 514.00 KiB/s, done.
Total 4 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/olliefr/rtc.git
   4999f8e..07e93a6  master -> master
```

The master project repository and the remote origin have now been updated.

## Cloning

To clone the master project, *including* the submodules, use `--recurse-submodules` parameter.

```Shell
$ git clone --recurse-submodules https://github.com/olliefr/rtc rtc
```

If you already cloned the project and forgot to recurse submodules, you still can clone the submodules with a one-liner.

```Shell
$ git submodule update --init
```

To print a list of submodules in the parent repository, use `git submodule status`

## Moar!

* `git-submodule(1)` and `gitsubmodules(7)` manual pages.
* The [Pro Git book](https://git-scm.com/book/en/v2) is rather good as well.

&mdash; Oliver Frolovs, 2020