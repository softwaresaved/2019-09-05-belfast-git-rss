# Version control for statistics

## Contents


* [Setting up a local repository](#setting-up-a-local-repository)
   * [Pre-checks](#pre-checks)
   * [Check that we have git in the shell](#check-that-we-have-git-in-the-shell)
   * [Getting help](#getting-help)
   * [Registering with git](#registering-with-git)
   * [Creating a repository](#creating-a-repository)
   * [First commit](#first-commit)
   * [More commits](#more-commits)
   * [Adding directories](#adding-directories)
   * [Changing a commit message](#changing-a-commit-message)
   * [Exploring history](#exploring-history)
   * [Ignoring files](#ignoring-files)
   * [Tagging](#tagging)
* [Creating remote repositories](#creating-remote-repositories)
* [Resources](#resources)

# Setting up a local repository

## Pre-checks

Make sure that:
* Your `~/.gitconfig` file has been temporarily moved.
* People can be paired up for the collaborative working.

## Check that we have git in the shell

Just to check that `git` is installed in the local machine.

```bash
$ git --version 
```

## Getting help

You can get help from `git` by just typing it at the command line.

```bash
$ git 
```

by itself returns most common commands. Same as:

```bash
$ git help 
```

You get an extended list of commands by doing:

```bash
$ git help --all
```

Want to know more about a command you can do:

```bash
$ git help add
```

which is the same as:

```bash
 $ git add --help
```

## Registering with git

You have to tell git who you are (only have to do this once per machine):

```bash
$ git config --global user.name "Mario Antonioletti"
$ git config --global user.email "mario@epcc.ed.ac.uk"
```

if you are going to use GitHub and want to keep your email private see [this page](https://help.github.com/en/articles/setting-your-commit-email-address).

Can also set:

```bash
$ git config --global color.ui "auto"
$ git config --global core.editor "nano -w"
```

You can see what configuration parameters you have 
set by doing:

```bash
$ git config -l
```

Putting entries into:

```bash
$ ls ~/.gitconfig
```

## Creating a repository

Let's create a repository:

```bash
 $ mkdir projectX
 $ cd projectX
```

Check what is there:

```bash
 $ ls -A
```

Initialise the repository:

```bash
 $ git init
```

Check to see what has changed:

```bash
 $ ls -A
```

Check the status of the repository.

```bash
 $ git status
```

## First commit

Edit a file (use an editor you are familiar with):

```bash
 $ nano README.md
```

For more information on using markdown see this [cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

Could add:

 > \# Project X

Check the state:

```bash
 $ ls
```

Check the file contents:

```bash
 $ cat README.md
```

and what is the repository status?

```bash
 $ git status
```

Workflow

    working directory --> staging area --> git repository
           ^                                     |
           |                                     |
           +-------------------------------------+

Add the file to the staging area:

```bash
$ git add README.md
```

Let's check the status:

```bash
 $ git status
```

Suppose you made a mistake and you want to unstage:

```bash
 $ git rm --cached README.md
```

Check:

```bash
 $ git status
```

## More commits

```bash
 $ git commit -m"Add information about my project."

 [master (root-commit) 18e86a7] Add information about my project.
  1 file changed, 2 insertions(+)
  create mode 100644 README.md
```

Check the status again:

```bash
 $ git status
```

If you do not specify the `-m` flag it will fire an editor for you.

```bash
 $ git log
```

Can have a shortened version of the commit log

```bash
 $ git log --oneline
```

Modify the text file:

 > \# Project X
 >
 > This project ...

 Check the contents:

```bash
 $ cat README.md
```

and the status:

```bash
$ git status
```

Suppose you can't remember what you changed, you can do:

```bash
$ git diff
```

If we add the file to the staging area:

```bash
$ git add README.md
```

If you do:

```bash
$ git diff
```

You can not see the difference because the file has been staged. However, you can do:

```bash
$ git diff --staged
```

Make more changes to show that there is a difference  between what is committed comes from the staging area and not the working copy.

## Adding directories

Cannot add directories by themselves:

```bash
mkdir data
git status
git add data
git status
```
you need to add a file - you can create a temporary file:

```bash
cd data
touch .gitkeep
ls
ls -a
git add .
git commit -m"Added directory for data."
```

Can get rid of the temporary files later.

## Changing a commit message

If you commit with a typo you can change:

```bash
$ git commit --amend -m "New message."
```

## Exploring history

Can do a diff with earlier versions:

```bash
git log --oneline
```

pick as specific revision and do:

```bash
git diff RevNum README.md
```

Can short hand this by:

```bash
git diff HEAD~N README.md
```

where the `N` signifies how many revisions back you want to go and `HEAD` points to the current version of the repository.

If you want the specific contents of a file at given revision you can do:

```bash
git show RevNum README.md
```

You make modifications to a file that you no longer want to keep:

```bash
$ git checkout -- README.md
```

Or you can even checkout earlier versions of the code:

```bash
$ git checkout RevNum -- README.md
```

If you want to recover the state of the repository you can go back
to `HEAD` by doing:

```bash
$ git reset --hard HEAD
```

## Ignoring files

You have seen that `git status` is a really useful command to  show you what has been changed. However if you have files that you do not want to put in the repository such as emacs back up  files, binary files, etc you can tell git to ignore these by creating a `.gitignore` file. In addition, you want to put the names of files that you NEVER want to commit into your repository that may have sensitive information, e.g. password files, sensitive data, etc. You can create this file and  add content that will apply recursively:

```bash
 *~
 .\#*
 \~*
 bin/
 passwds/
```

add and commit this file and you will reduce the clutter you get.

```bash
$ git add .gitignore
$ git commit -m".gitignore: files to ignore."
```

git will not let you commit files that are contained in the `.gitignore` file.

## Tagging

Can put a human readable version. Lightweight tag:

```bash
$ git tag v0.1
$ git tag             # Lists available tags
$ git show v0.1       # gives you information about the commit
```

We can do some more edits and do an annotated tag:

```bash
$ git tag -a v1.0 -m"First release."
$ git show v1.0
```

Use lightweight tags for your own use and annotated tags for the benefit of others.



# Creating remote repositories

# Resources

