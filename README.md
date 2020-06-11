# Learn Git the Easy Way

This is a simple, guided tutorial intended to be a simple introduction to Git. While other tutorials may concentrate on terminal commands and Git objects, this guide sticks to the basics. In this tutorial, we will go through an introduction to Git and version control, a breakdown of how to use Git, and a sample project with Github Desktop to demonstrate the practical usage of Git. If you have no experience, don't worry! This tutorial assumes no knowledge of the CLI or programming. Enjoy!

---

## Introduction

### What is Git?

Git is a version control system. Version control systems (VCSs) are tools used to track changes to source code (or other collections of files and folders). As the name implies, these tools help maintain a history of changes; furthermore, they facilitate collaboration. VCSs track changes to a folder and its contents in a series of snapshots, where each snapshot encapsulates the entire state of files/folders within a top-level directory. VCSs also maintain metadata like who created each snapshot, messages associated with each snapshot, and so on.

Why is version control useful? Even when you’re working by yourself, it can let you do the following and much more:

- look at old snapshots of a project
- keep a log of why certain changes were made
- work on parallel branches of development

When working with others, it’s an invaluable tool for seeing what other people have changed, as well as resolving conflicts in concurrent development.

Modern VCSs also let you easily (and often automatically) answer questions like:

- Who wrote this code?
- When was this particular line of this particular file edited? By whom? Why was it   edited?
- Over the last 1000 revisions, when/why did a particular test stop working?

While other VCSs exist, Git is the de facto standard for version control. [This XKCD comic](https://xkcd.com/1597/) captures Git’s reputation:

![](https://imgs.xkcd.com/comics/git_2x.png)

The above was sourced from [The Missing Semester of Your CS Education](https://missing.csail.mit.edu/2020/version-control/).

### Git vs. Github

Before we begin, it is important to separate **Git** and **Github** from one another.

- [Git](https://git-scm.com/) is a free and open source VCS created by [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds).

- [Github](https://github.com/) is a Git repository hosting service that uses Git under the hood. Beyond just hosting Git repositories, Github also adds the following:

    - a pretty Web UI
    - *forking* (copying someone's repository)
    - *pull requests* (requesting a change to someone's repository)
    - *merging* (approving a pull request)
    - other ancillary services like project boards, wikis, issues, CI/CD (Github Actions), etc

Before Github, if you wanted to contribute to someone else's repository you had to download it, make your changes, and email them to the maintainer who could merge them into their upstream copy. With Github, changes can be submitted, discussed, and collaborated on in a public, trackable manner.

The important thing to remember is that **Git is not the same as Github**, and Github is just one of many [Git hosting providers](https://itsfoss.com/github-alternatives/).

---

## Using Git

### What is a Git Repository?

A Git repository is a folder containing all of the files pertaining to a project. Generally, the idea is that Git tracks the version history every file in that folder (excluding those specified in a `.gitignore` - this will come later). The data of a Git repository is stored in a subfolder named `.git` in the repository folder.

A Git repository can either exist solely locally (on your computer) or it can have a remote. A remote repository is version of the project that is hosted on the internet. By having a remote (an example being a repository on Github) multiple people working on a repository can agree on a common version of that repository. In most cases, everyone working on a project uses the same remote. The basic workflow is as follows:

1. Create a repository locally
2. Sync that repository to a remote
3. Other people download copies of the repository
4. Everyone makes changes
5. Changes get pushed to the remote and conflicts get resolved either automatically or manually

Conflicts usually are mitigated through several strategies, but that is beyond the scope of this guide. Simply put, most conflicts can be resolved by having people push their changes to the remote at different times and having different copies of the remote (called branches) that people can work on separately until it is time to merge those changes into the base version of the repository.

### Git Commands

The following are the most commonly used commands in Git. The term 'commands' is used because Git is traditionally a command line tool; instead of clicking a button to create a repository a programmer would type `git init`. However, this tutorial covers using Git with Github Desktop, a GUI for Git. As such, the names of the textual commands will be used, but their meanings will also be explained so they make sense with any way of interacting with Git.


#### git init

**CLI:** `git init`

**Github Desktop:** `File > New Repository` *or* `Ctrl + N`

**What does it do?**
The `git init` command reates a new repository in the current directory (or directory specified in the Github Desktop GUI). Essentially, all that is happening is a `.git` directory is created and put in the directory specified. The existing files in the directory are not affected.


#### git clone

**CLI:** `git clone <repo>`

**Github Desktop:** `File > Clone Repository` *or* `Ctrl + Shift + O`

**What does it do?**
The `git clone` command is primarily used to point to an existing repo and make a clone or copy of that repo at in a new directory, at another location. The original repository can be located on the local filesystem or on remote machine accessible by supported protocols. The `git clone` command copies an existing Git repository.


#### git add

**CLI:** `git add <pathspec>`

**Github Desktop:** Under the Changes tab, select the checkbox next to a changed file

**What does it do?**
The `git add` command adds a change in the working directory to the staging area. It tells Git that you want to include updates to a particular file in the next commit. However, `git add` doesn't really affect the repository in any significant way—changes are not actually recorded until you run `git commit`.


#### git commit

**CLI:** `git commit`

**Github Desktop:** At the bottom left of the screen, click `Commit to <branch>`

**What does it do?**
The `git commit` command captures a snapshot of the project's currently staged changes. Committed snapshots can be thought of as “safe” versions of a project—Git will never change them unless you explicitly ask it to. Prior to the execution of `git commit`, The `git add` command is used to promote or 'stage' changes to the project that will be stored in a commit. These two commands `git commit` and `git add` are two of the most frequently used.


#### git fetch

**CLI:** `git fetch`

**Github Desktop:** On the panel right below the top of the screen, click `Fetch Origin`

**What does it do?**
The `git fetch` command downloads commits, files, and refs from a remote repository into your local repo. Basically, it retrieves the latest changes from a remote without changing the local copy.


#### git pull

**CLI:** `git pull`

**Github Desktop:** On the panel right below the top of the screen, after fetching click `Pull Origin` *or* `Repository > Pull` *or* `Ctrl + Shift + P`

**What does it do?**
The `git pull` command is used to fetch and download content from a remote repository and immediately update the local repository to match that content.


#### git push

**CLI:** `git push`

**Github Desktop:** On the panel right below the top of the screen, after making local commits click `Push Origin` *or* `Repository > Push` *or* `Ctrl + P`

**What does it do?**
The `git push` command is used to upload local repository content to a remote repository. Pushing is how you transfer commits from your local repository to a remote repo.


#### git branch

**CLI:** `git branch`

**Github Desktop:** `Branch > New Branch` *or* `Ctrl + Shift + N`

**What does it do?**
A branch represents an independent line of development. Branches serve as an abstraction for the edit/stage/commit process. You can think of them as a way to request a brand new working directory, staging area, and project history. New commits are recorded in the history for the current branch, which results in a fork in the history of the project.
The `git branch` command lets you create, list, rename, and delete branches.


#### .gitignore

Ignored files are tracked in a special file named `.gitignore` that is checked in at the root of your repository. There is no explicit git ignore command: instead the `.gitignore` file must be edited and committed by hand when you have new files that you wish to ignore. `.gitignore` files contain patterns that are matched against file names in your repository to determine whether or not they should be ignored. In short, **you can list the names of files you don't want tracked in the `.gitignore` file.**

The Git command descriptions above were sourced from [Learn Git with Bitbucket Cloud](https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud).

---

## Git project with Github Desktop

### Github Desktop

The fact that this guide will use Github Desktop is noted several times above, without being explained much further. Github Desktop is an open source Git client designed by Github. Before continuing, it is very important to understand that Github Desktop is primarily designed to work with Github. In Github's [explanation of Desktop](https://github.com/desktop/desktop/blob/development/docs/process/what-is-desktop.md), they say the following:

> It is intended primarily to extend the features of GitHub, not to be an agnostic Git client or replicate the feature set of github.com. While we support very basic functionality that will allow the app to function with other hosting providers, we prioritize work that allows the end-to-end GitHub and GitHub Enterprise experience to shine and takes advantage of the fact that we can closely integrate with GitHub features.

In other words, Github Desktop is mostly suitable as a beginner tool, and moving beyond the functionality described in this tutorial should be done with either a hosting provider agnostic Git GUI or the Git CLI.

### Project

This project is very simple. You will fork this repository, clone it to your machine, create a new branch, make a change, commit that change, push the change, and finally make a pull request into the master branch of the main repository. To get started, download [Github Desktop](https://desktop.github.com/).

#### 1. Clone the repository

Clone this repository by selecting `URL` in the pop up window and entering `The-Kid-Gid/learn-git`.

#### 2. Create a new branch

Create a new branch named `myname_rewrite` and select the option `Publish your branch`. When prompted whether you want to fork the repository, select `Fork this repository`, then select `To contribute to the parent project`.

#### 3. Make your change

Create a new file called `myname_contributed.txt` in the `contributors` directory.

#### 4. Commit your change

Now, on the left side of Github Desktop, you should see `1 changed file` above the path to the new file. Under that title your commit, optionally add a description, and click `Commit to myname_rewrite`.

#### 5. Push your change

You should see a prompt that says `Push commits to the origin remote`. Either click the button labelled `Push origin` next to it or push some other way.

#### 6. Create a pull request

Now you have your own version of the learn-git repository, but you need to merge your changes from the head repository (your fork) to the base repository (The-Kid-Gid/learn-git). Github Desktop has a handy way to do this by just clicking `Create Pull Request`. Once you do so it will take you to the Github website, where you can title, describe, and file your PR.

Congratulations! You now have a basic understanding of Git. Keep in mind that Github Desktop is not a tool oriented towards more advanced workflows, and if you find yourself being limited by it your best option is to learn the Git CLI. Some of the best resources for doing so are the free [Pro Git](https://git-scm.com/book/en/v2) book hosted on git-scm.com and [Learn Git with Bitbucket Cloud](https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud) by Atlassian.