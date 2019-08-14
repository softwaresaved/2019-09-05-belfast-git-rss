# Version control for statistics



## Contents

* [Setting up a local repository](#setting-up-a-local-repository)
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

# Resources

