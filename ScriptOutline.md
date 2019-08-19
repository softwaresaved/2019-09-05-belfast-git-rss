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

   * [Creating a remote repository](#creating-a-remote-repository)
   * [Pulling remote changes](#pulling-remote-changes)
   * [Pushing local changes](#pushing-local-changes)
   * [Pulling before you push](#pulling-before-you-push)
   * [Resolving a conflict](#resolving-a-conflict)
   * [Who to Blame](#who-to-blame)
   * [Adding collaborators](#adding-collaborators)
   * [Exercise 2](#exercise-2)
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

We use GitHub. We are going to create a remote repository on GitHub and then push our local content.

1. Go to [http://github.com](http://github.com/).
2. Login (if you have not created an account you will have to sign up).
3. Click on the `+` and choose `New repository`.
4. Choose a name for your repository, e.g.  `projectX`.
5. Follow the instructions under the heading `…or push an existing repository from the command line`.
6. Follow the instructions there.
7. Click on `Overview` on the left hand menu and you should see your file together with the commits.
8. Click on source and you should be able to browse your sources.

Only do this if the above worked without error. Now, go outside your local git repo:

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

The contents will then be saved to `OtherName`.

## Pulling remote changes

On the remote repository you can make changes by clicking on the file that you wish to edit and then clicking on the pencil on the top right of the frame surrounding the file that you are viewing. 

* Click on the pencil.
* Make a change.
* Go to the bottom of the file and commit the file with a sensible commit message.

Your remote repository and local repository are different. To reconcile them in **your local repository** (make sure you are in the repository) do:

```bash
git pull
```

This will fetch the contents of the remote repository and try to do a merge with your local conent. A `git pull` is the same is the same as doing a `git fetch` and a `git merge` in one go.

If the `git pull` works correctly, then the two repositories should be identical. 

## Pushing local changes

Now make a change in your local git repository:

* Edit the `Readme.md` file.
* Do a `git add`
* Do a `git commit`

Now the local repository is not reconciled with the remote repository. In order to synchronise both repositories in your local repository do:

```bash
git push
```

So now you know how to pull your changes from your remote repository to your local changes and how to push your local changes to the remote repository.

## Pulling before you push

Now do a change in the remote repository (change the title say) and also in the local repository (add a paragraph at the bottom of the file, make sure that your changes are in different locations of the file). Now try to reconcile the repositories by doing a push from the local to the remote repositories (it will fail):

```bash
git push
To YourRepoURL
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'YourRepoURL'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

If the remote repository has changed you MUST pull the remote changes to your local repository and reconcile any conflicts (we cover that next). So you need to do:

```bash]
git pull   # Pull the changes
git push   # If all went well with the pull
```



## Resolving a conflict

git can merge text files if the changes happen in different locations. However, if the changes happen in the same line or roughly the same region then you have to resolve the conflict. Suppose we change the same line in both your local and remote repositories, say the title then when you do a pull you will see something like:

```bash
git pull
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From YourRepositoryURL
   94a1451..00e44e8  master     -> origin/master
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

If you look inside the file you will see:

```bash
<<<<<<< HEAD
# This is a new title


=======
# This is the original title
>>>>>>> 00e44e8974c0bfa7aff5dd3cb296a6be6ccea128
```

The first version , call this version A, is what is in your local repository. The version that is beow the `=======`, version B, is what was in the remote repository.  There may be one or more regions of conflict thus:

```bash
<<<<<<< HEAD

version A
=======

version B

>>>>>>> Some Has String
```

Your role, for each region of conflict,  is to choose Version A or Version B, a combination of both or neither but you need to get rid of the less than separators, the equal signs and the greater than signs. If you are collaborating you should talk to your collaborator. Suppose we want to keep version A. We then change the text to be:

```bash
# This is a new title
```

We then add and commit the file:

```bash
git add Readme.md
git commit -m"Resolved the title conflict."
git push
```

You would have to do that for every conflict (can sort out individually or in one go).

## Who to Blame

If you are collaborating with various people you may want to find out who made changes to what bit of the file and when. To do this you can use the `git blame` command:

```bash
git blame Readme.md
8e33b5ce (Mario Antonioletti 2019-07-10 12:30:55 +0100  1) # RSS 2019 International Conference
8e33b5ce (Mario Antonioletti 2019-07-10 12:30:55 +0100  2) ## Data Science: Version control for statistics
8e33b5ce (Mario Antonioletti 2019-07-10 12:30:55 +0100  3) ### Belfast, 5th September 2019
42722c97 (Mario Antonioletti 2019-06-07 17:29:34 +0100  4)
45a95fd2 (Mario Antonioletti 2019-06-07 17:33:33 +0100  5) This page is for the [RRS 2019 International conference](https://www.rss.org.uk/RSS/Events/RSS_Conference/2019_Conference/RSS/Events/Conference/2019_conference.aspx?hkey=2a432b6b-6baf-4bc3-baa4-063221c13ab8) for the [Data Science: Version control for statistics (part 1)](https://events.rss.org.uk/rss/frontend/reg/titem.csp?pageID=104517&eventID=270) and [Data Science: Version control for statistics (cont)](https://events.rss.org.uk/rss/frontend/reg/titem.csp?pageID=108408&eventID=270) workshops.
42722c97 (Mario Antonioletti 2019-06-07 17:29:34 +0100  6)
42722c97 (Mario Antonioletti 2019-06-07 17:29:34 +0100  7) ## Learning objectives
8b1d8347 (Mario              2019-07-11 13:39:47 +0100  8)
...
```

This gives you:

* The revision of when the change  was made
* Who made the change
* When they made the change
* The line number of the file
* The contents of the line

Clearly this command will be of more use when multiple users are editing the same files.

## Adding collaborators

You will only do the following with people that you really trust. You will be paired up with another attendee. One of you will be `user 1` and the other will be `user 2`.  `User 2` will be your collaborator. 

### Instructions for `User 1`

Go to your GitHub remote repository web page. Then:

* Click on `Settings`.
* On the `Options` menu on the left click on`Collaborators & teams`.
* You will have to confirm your password.
* Find out the GitHub id of your collaborator.
* Enter it into the `Add collaborators` search box.
* Press on `Add collaborator`.

## Instructions for `User 2`

For `user 2` you should get an email from `User 1` to become a collaborator:

* Go to the URL in the email or get the URL of their repository from `user 1`.
* You will see a green button on the top right that says: `Clone or download`. Click on this, make sure you have the `Clone with https` option. Copy the URL.
* On your shell now make sure that you are not in an existing git repository. To make sure type:

```bash
git status
fatal: not a git repository (or any of the parent directories): .gitbash
```

and you are then safe. If you are still in an existing git repository do a `cd ..` until you see the above error message. Then clone `User 1`'s repository:

```bash
git clone URLofRemoteRepo/projectx.git
```

If you already have a `projectx`repo with the other name add an extra arguement to the above command, viz:

```bash
git clone URLofRemoteRepo/projectx.git projecty
```

which will call the repo `projecty` (you can choose whatever name you wish). Change directory into this repository. You are now ready to do the exercise.

## Exercise 2

In this exercise `user 1` and `user 2` will be collaborating in the same repo. Make changes to the `Readme.md`, add new files, remember to do a `git pull` and `git push`. Use `git blame` to see who made what changes. Resolve any conflicts if these arise.

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
