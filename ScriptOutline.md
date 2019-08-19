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
   * [Exercise 1](#exercise-1)
   * [Adding directories](#adding-directories)
   * [Changing a commit message](#changing-a-commit-message)
* [Creating remote repositories](#creating-remote-repositories)
* [Back to local repositories](#back-to-local-repositories)

   * [Exploring history](#exploring-history)
   * [Ignoring files](#ignoring-files)
   * [Tagging](#tagging)
* [Branching](#branching)

   * [Removing a remote repository](#removing-a-remote-repository)
* [Resources](#resources)

# Setting up a local repository

## Pre-checks

These are a reminder for the instructor. Make sure that:
* Your `~/.gitconfig` file has been temporarily moved.
* People can be paired up for the collaborative working.

## Check that we have git in the shell

Just to check that `git` is installed in your local machine.

```bash
git --version 
```

## Getting help

You can get help from `git` by just typing it at the command line.

```bash
git 
```

by itself returns most common commands. Same as:

```bash
git help 
```

You get an extended list of commands by doing:

```bash
git help --all
```

Want to know more about a command you can do:

```bash
git help add
```

which is the same as:

```bash
git add --help
```

## Registering with git

You first have to tell git who you are and your contact details (you only have to do this once per machine):

```bash
git config --global user.name "Mario Antonioletti"
git config --global user.email "mario@epcc.ed.ac.uk"
```

if you are going to use GitHub and want to keep your email private see [this page](https://help.github.com/en/articles/setting-your-commit-email-address).

You can also set other defaults:

```bash
git config --global color.ui "auto"
git config --global core.editor "nano -w"
```

You can see what configuration parameters you have set by doing:

```bash
git config -l
```

Putting entries into:

```bash
ls ~/.gitconfig
```

## Creating a repository

Let's create a repository. Start by creating a new directory:

```bash
mkdir projectX
cd projectX
```

Check what is there:

```bash
ls -A
```

Initialise the repository:

```bash
 git init
```

Check to see what has changed:

```bash
 ls -A
```

You can remove the repository status by removing the `.git` directory.

Check the status of the repository:

```bash
 git status
```

## First commit

Edit a file (use an editor you are familiar with):

```bash
 nano README.md
```

The `md` extension is usually used for markdown. For more information on using markdown see this [cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

Could add:

 > \# Project X

Check the state:

```bash
ls
```

Check the file contents:

```bash
cat README.md
```

and what is the repository status?

```bash
git status
```

Workflow

    working directory --> staging area --> git repository
           ^                                     |
           |                                     |
           +-------------------------------------+

Add the file to the staging area:

```bash
git add README.md
```

Check the status of the repository:

```bash
git status
```

Suppose you made a mistake and you want to unstage:

```bash
git rm --cached README.md
```

Check:

```bash
 git status
```

## More commits

```bash
git commit -m"Add information about my project."

 [master (root-commit) 18e86a7] Add information about my project.
  1 file changed, 2 insertions(+)
  create mode 100644 README.md
```

Check the status again:

```bash
git status
```

If you do not specify the `-m` flag it will fire an editor for you expecting you to add a commit message.

```bash
git log
```

Can have a shortened version of the commit log:

```bash
git log --oneline
```

Modify the text file:

 > \# Project X
 >
 > This project ...

 Check the contents:

```bash
cat README.md
```

and the status:

```bash
git status
```

Suppose you can't remember what you changed, you can do:

```bash
git diff
```

If we add the file to the staging area:

```bash
git add README.md
```

If you do:

```bash
git diff
```

You can not see the difference because the file has been staged. However, you can do:

```bash
git diff --staged
```

Make more changes to show that there is a difference  between what is committed comes from the staging area and not the working copy.

## Exercise 1

Do some additional changes to your repository. Do some more changes to the `Readme.md` file. Try adding and committing some new files.

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
git commit --amend -m "New message."
```

# Creating remote repositories

There are a number of external git repositories hosts you can use if your local institution does not have one.

| Provider  | URL                                                   |
| --------- | ----------------------------------------------------- |
| GitHub    | [https://github.com](https://github.com/)             |
| GitLab    | [https://about.gitlab.com](https://about.gitlab.com/) |
| BitBucket | https://bitbucket.org/product                         |
| ...       | ...                                                   |

There are more, all services are roughly similar but for the free service these offer advantages/disadvantages in different areas. For a more a more exhaustive comparison see this [wikipedia article](https://en.wikipedia.org/wiki/Comparison_of_source-code-hosting_facilities). Without prejudice we shall be using GitHub.

## Creating a remote repository

We will use GitHub. We are going to create a remote repository on GitHub and push our content.

1. Go to [http://github.com](http://github.com/).
2. Login (if you have not created an account you will have to sign up).
3. Click on the `+` and choose `New repository`.
4. Choose a name for your repository `projectX`.
5. Use `…or push an existing repository from the command line`.
6. Follow the instructions there.
7. Click on `Overview` on the left hand menu and you should see your file together with the commits.
8. Click on source and you should be able to browse your sources.

Now, go outside your git repo:

```bash
cd ..           # Go outside your repository.
rm -fr projectx # Be very careful with this command.
```

Now we recover your repository by doing:

```bash
git clone https://github.com/YourId/YourProjectName.git
```

Make sure that:

* You are not inside another git repository.
* If you have an existing directory with the same name (without the `.git` extension) then you can clone to another directory by giving it another name at the end.

```bash
git clone https://github.com/YourId/YourProjectName.git OtherName
```

The contents will then be saved to `OtherName`

# Back to local repositories

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
git checkout -- README.md
```

Or you can even checkout earlier versions of the code:

```bash
git checkout RevNum -- README.md
```

If you want to recover the state of the repository you can go back
to `HEAD` by doing:

```bash
git reset --hard HEAD
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
git add .gitignore
git commit -m".gitignore: files to ignore."
```

git will not let you commit files that are contained in the `.gitignore` file.

## Tagging

Can put a human readable version. Lightweight tag:

```bash
git tag v0.1
git tag             # Lists available tags
git show v0.1       # gives you information about the commit
```

We can do some more edits and do an annotated tag:

```bash
git tag -a v1.0 -m"First release."
git show v1.0
```

Use lightweight tags for your own use and annotated tags for the benefit of others.

# Branching

Branching allows a very powerful way of forking your code. Suppose you want to instrument it for performance analysis or you are collaborating and you do not want to be modifying the same code at the same time. Unlike CVS and SVN branches are really cheap and uncomplicated.

Can use to:

* Explore/deveop a new feature
* Stop developers clashing on development
* Create a particular branch, a version of a release

Let's write a bit of Python code to demonstrate `hello.py`:

```python

print("Hello World!")

```

Run the code `python hello.py`. Now suppose you want to instrument the code (put in timing calls). You do not want to do this in your master branch:

```bash
git branch           # list the branches available, only master
git branch profile   # Creates the new branch:
git checkout profile # Change to the new branch
```

Now change the code:

```python
import time

start = time.time()

print("Hello World!)

end = time.time()

print("Code took ",(end - start)," seconds)
```

Execute the code. Add, commit. 
Go back to the master branch.
Change the original code.

```python

print("Hello World!")
print("I am a real programer now!")

```
Execute, add, commit. 

```bash
git checkout profile
cat `hello.py`    # Execute
git log --oneline # Check local changes
git log --oneline master # Check changes on the master branch
git merge master  # Incorporate changes from the maser branch
```

Make a change on the `Hello World` line. Execute, add, commit. Change
back to the master branch. Change the same line, execute, add and commit.
Go back to the profile branch and try to do a `merge` which should result
in a conflict. Show how to resolve the conflict.

To push the branch to the remote repository:

```bash
git push origin profile
```

## Removing a remote repository
If you do not wish to keep the remote test repository that you created you can remove it by:

1. Go to the repository page on GitHub.
2. On the top right you will see a gear wheel with the label `Settings`, click on that.
3. Scroll down to the bottomo of this page to the `Danger Zone`, you will see a button to `Delete this Repository`, click on that.
4. You will be asked to confirm the name of the repository, once you confirm your remote repository will be removed.

You still have your local repository (unless you choose to remove that as well).
# Resources

* 

<br/>
<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons Licence" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br/>
This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">
Creative Commons Attribution 4.0 International License</a>.
