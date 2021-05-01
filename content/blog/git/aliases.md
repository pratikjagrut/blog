---
title: "Git aliases"
description: ""
date: 2021-04-29T08:23:36+05:30
draft: false
author: "Pratik Jagrut"
layout: "blog"
images:
  - src: "img/git/aliases.jpg"
    alt: "git aliases"
    # stretch: "horizontal"
    removeBlur: true
categories:
  - "git"
tags:
  - "git"
  - "programming"
---
Git is the most widely used ***`Version Control System (VCS)`*** or ***`Source Code Management(CMS)`*** software.
It is a day-to-day go-to tool for many of the developers out there.
And many developers use terminal/command line to operate it.

In the terminal we type git commands ***`git <sub-command> <flag>`*** it runs if it succeeds we're happy.
On day-to-day basis we mostly use repetitive commands like ***`git pull <remote> <branch>`***, ***`git push <remote> <branch>`***, ***`git commit`*** and many other and sometimes we use prolonged commands like this one ***`git log --graph --pretty=format:'%Cred%h%Creset %Cgreen%cr%Creset -%C(yellow)%d%Creset %s %C(bold blue)[%cn]%Creset' --abbrev-commit --date=relative`*** which prints commit history in custom fashion.

Typing those repetitive or lengthy, complex commands with too many arguments could be erroneous and could decrease our efficiency ensuing less productivity.

In this article, we'll learn how to run Git command efficiently and develop a more productive Git workflow using Aliases.

***NOTE: The aliases in this article are my personal choice influenced by my day-to-day Git interaction.***
## What is an alias?

Aliases are short commands assigned to a particular command. It can be visualized as a shortcut for any command.

Creating an alias serves some basic needs:

- It helps to shorten the lengthy command and saves us from tedious, erroneous typing.

- It saves us from memorizing complex commands.

- Creates abridged commands for regularly used commands ensuing in an increase in productivity.

***We can use two types of aliases for Git commands:***

- Bash alias
- Git alias 

We'll look into both.

## Bash Alias

Defining a bash alias is a simple task. Below is a command for it.

```
alias g='git'
```

And done, we've `g` as an alias for the `git` command.

But this alias is not persistent as soon as you end the terminal session the alias is gone. 
To make it persistent we've to add this alias in ***`.bashrc`*** if you use the bash shell or ***`.zshrc`*** if you use zsh. 
These files are mostly located in you're home directory.

To know what shell you're using type echo 

```
echo "$SHELL"
/usr/bin/zsh
```

For the git command, I've two bash aliases `g` and `gt`. 
Sometimes due to old habit, I tend to type `git` instead of `g` and while doing that sometimes I miss the `i` in `git` so to avoid throwing an error I added `gt` as an alias in `.zshrc`.

```
alias g='git'
alias gt='git'
```
## Git alias

To define a git alias we use the ***`git config`*** command.
We can define two types of aliases in Git.

- ***`Global aliases`***, which are stored in ***`.gitconfig`*** file which is mainly located in the home directory. These aliases are available to all git repositories present in the system. Command to define global alias:  
  
  ```
  git config --global alias.<alias_name> '<command>'
  ```
  ```
  or you can directly edit the .gitconfig file.
  ```

- ***`Local aliases`***, which are stored in ***`.git/config`*** file of the particular project. These aliases are not available to any other repository. Command to define local alias:
  ```
  git config alias.<alias_name> '<command>'
  ```
  ```
  or you can directly edit the .git/config file.
  ```

### Some useful git aliases

- #### Git Status

    ***`git status`*** is a command which is used very frequently to see changed or untracked files.
    ```
    git config --global alias.st 'status'
    ```
    So now instead of ***`git status`*** we can just type ***`git st`*** or ***`g st`*** if bash alias ***`g=git`*** is set. 
    This is the benefit of using aliases, the whole command can be converted into few characters.
    ```
    $ g st
    On branch master
    Your branch is up to date with 'origin/master'.

    nothing to commit, working tree clean
    ```
    The git will store this alias in .gitconfig file under `[alias]` section as `st = status`.
  
- #### Git Pull

  ***`git pull <remote> <ref/branch>`*** this command pulls the code from specified remote branch.
  ```
  git config --global alias.pl 'pull'
  ```
  Now the pull command will be ***`git pl <remote> <ref/branch>`***.

  We can shorten it further depending on remote and branch.
  ```
  git config --global alias.plo 'pull origin'
  ```
  Now the command ***`git plo main`*** is the same as ***`git pull origin main`***.

  We can create dedicated alias for ***`git pull origin main`***
  ```
  git config --global alias.plom 'pull origin main'
  ```
  Now the entire command is abridged, ***`git plom`***.

- #### Git Checkout

  ***`git checkout`*** Switch branches or restore working tree files.
  ```
  git config --global alias.co 'checkout'
  ```
  Now we can use ***`git co <branch>`*** to checkout that branch.

  To create new branch we use ***`git checkout -b <new_branch> <start_point>`***
  ```
  git config --global alias.cnb 'checkout -b'
  ```
  So now we can ues ***`git cnb <new_branch> <start_point>`***

- #### Git Branch

  ***`git branch`*** List, create, or delete branches
  ```
  git config --global alias.br 'branch'
  ```
  ```
  $ git br

  * branch1
  main
  ```
- #### Git add

  ***`git add <pathspec>...`*** adds file contents to the index
  ```
  git config --global alias.a 'add'
  ```
  The command will be `git a <pathspec>...`

  To add all the files (changed + untracked) we can do ***`git add .`***.
  ```
  git config --global alias.aa 'add .'
  ```
  Now to add all files we can use ***`git aa`***
  
- #### Git commit

  After adding files to the index we use ***`git commit`*** to record changes to the repository.
  For git commit alias could be:
  ```
  git config --global alias.ci 'commit'
  ```
  ```sh
  $ git ci

  [update.theme 89f083e] Update CR yaml
  1 file changed, 1 insertion(+)
  create mode 100644 cr.yaml
  ```

- #### Git push

  Once your changes are committed and you need to update the remote reference with new changes we use ***`git push <remote> <branch>`***
  ```
  git config --global alias.p 'push'
  ```

  We can shorten it further depending on remote and branch.
  ```
  git config --global alias.po 'push origin'
  ```
  Now the command ***`git po main`*** is the same as ***`git push origin main`***.

  We can create dedicated alias for ***`git push origin main`***
  ```
  git config --global alias.pom 'push origin main'
  ```
  Now the entire command is abridged, ***`git pom`***.

- #### Git log 

  ***`git log`*** is one of the most important commands in git. It shows us the commit history.
  Now there are various ways of seeing commit history, depending on how we wanna see commit history we can use the flags.

  I usually use these three aliases for log.

  This alias shows complete commit logs with the addition and deletion stats.
  ```
  git config --global alias.lg 'log --stat'
  ```
  ```
  $ git lg
  
  commit 8b6ac3a9789002a2c578139c830f17b9e18b53f7 (HEAD -> git.aliases, origin/main, origin/HEAD, update.theme)
  Author: Pratik Jagrut <26519653+pratikjagrut@users.noreply.github.com>
  Date:   Sat May 1 21:47:48 2021 +0530

      Update public directory

  public | 2 +-
  1 file changed, 1 insertion(+), 1 deletion(-)
  ```

  This alias draws a text-based graphical representation of the commit history printed in between commits with relative time.
  ```
  git config --global alias.lgdr "log --graph --pretty=format:'%Cred%h%Creset %Cgreen%cr%Creset -%C(yellow)%d%Creset %s %C(bold blue)[%cn]%Creset' --abbrev-commit --date=relative"
  ```
  ```
  $ git lgdr

  * 8b6ac3a 6 hours ago - (HEAD -> git.aliases, origin/main, origin/HEAD, update.theme) Update public directory [Pratik Jagrut]
  * f47c1c6 6 hours ago - Update theme [Pratik Jagrut]
  ```

  This alias draws a text-based graphical representation of the commit history printed in between commits with a short format of the date.
  ```
  git config --global alias.lgds "log --graph --pretty=format:'%Cred%h%Creset %Cgreen%cr%Creset -%C(yellow)%d%Creset %s %C(bold blue)[%cn]%Creset' --abbrev-commit --date=short
  ```
  ```
  $ git lgds

  * 8b6ac3a 2021-05-01 - (HEAD -> git.aliases, origin/main, origin/HEAD, update.theme) Update public directory [Pratik Jagrut]
  * f47c1c6 2021-05-01 - Update theme [Pratik Jagrut]
  ```

<b style="color:#3269a8"><i>These were some of the aliases from my list, you can make more aliases for sub-commands like branch, remote, diff, config, etc...</i></b>

## Conclusion

Git aliases are a very useful feature. They help to improve the overall efficiency and productivity of git workflow. 
We can define as many aliases as we want, Git is too generous. It is always good to have aliases for regularly used and lengthy commands.

<b style="color:#cc3300"><i>***Thank you for reading this blog please give your feedback in the comment section below.***</i></b>
<hr>