# No-SSH approach for GitHub under Linux

I wanted to make full use of my `git` repositories on [GitHub](https://github.com/) without having to set up SSH access. I'm using [Ubuntu Linux](https://ubuntu.com/) under [WSL](https://docs.microsoft.com/en-gb/windows/wsl/).

## Setting up

* Use GitHub web interface to create a [new personal access token](https://github.com/settings/tokens/new) with the scopes `repo` and `gist`. **Copy the token value** into the clipboard as it won't be displayed more than once.
* On the local Linux host, configure `git` to store authentication information:
  
  ```Shell
  [~]$ git config --global credential.helper store
  ```
* Edit `~/.git-credentials` to include the following line, with `USER` being your GitHub username and `TOKEN` the value of the token in the clipboard.
  
  ```
  https://USER:TOKEN@github.com
  ```
  
* Make sure the credentials file is readable only by yourself:
  ```Shell
  [~]$ chmod 400 .git-credentials
  ```

## Usage

The following is a test I've conducted after setting up access as described in the previous section.

* Clone a *private* repository:
  
  ```Shell
  $ git clone https://github.com/olliefr/memes
  Cloning into 'memes'...
  remote: Enumerating objects: 111, done.
  remote: Counting objects: 100% (111/111), done.
  remote: Compressing objects: 100% (103/103), done.
  remote: Total 111 (delta 18), reused 97 (delta 7), pack-reused 0
  Receiving objects: 100% (111/111), 5.05 MiB | 7.54 MiB/s, done.
  Resolving deltas: 100% (18/18), done.
  ```

* *Update a file...*
  
* Push the changes to GitHub:
  
  ```Shell
  $ git push origin master
  Enumerating objects: 5, done.
  Counting objects: 100% (5/5), done.
  Delta compression using up to 12 threads
  Compressing objects: 100% (3/3), done.
  Writing objects: 100% (3/3), 335 bytes | 335.00 KiB/s, done.
  Total 3 (delta 1), reused 0 (delta 0)
  remote: Resolving deltas: 100% (1/1), completed with 1 local object.
  To https://github.com/olliefr/memes.git
     ae27d9c..c75a43e  master -> master
  ```

Yay!

## More information

* I picked up the idea for this worklow from the *Pro Git* chapter [*Credential Storage*](https://git-scm.com/book/en/v2/Git-Tools-Credential-Storage).

Relevant GitHub documentation pages:

* [Which remote URL should I use?](https://docs.github.com/en/github/using-git/which-remote-url-should-i-use) &mdash; convince yourself you don't need SSH.
* [About authentication to GitHub](https://docs.github.com/en/github/authenticating-to-github/about-authentication-to-github)
* [Creating a personal access token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)


&mdash; Oliver Frolovs, 2020