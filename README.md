# Learn Git the Easy Way

This is a simple, guided tutorial intended to be a simple introduction to Git. 
While other tutorials may concentrate on terminal commands and Git objects, this guide sticks to the basics. 
In this tutorial, we will go through an introduction to Git and version control, a breakdown of how to use Git, and a sample project with GitHub Desktop or the command line interface (CLI) to demonstrate practical usage of Git. 
If you have no experience, don't worry! This tutorial assumes no knowledge of the CLI or programming. Enjoy!

## Table of Contents

- **[Introduction](#introduction)**
    - **[What is Git?](#what-is-git)**
    - **[Git vs. GitHub](#git-vs-github)**
- **[Using Git](#using-git)**
    - **[What is a Git Repository?](#what-is-a-git-repository)**
    - **[Git Commands](#git-commands)**
        - **[git init](#git-init)**
        - **[git clone](#git-clone)**
        - **[git add](#git-add)**
        - **[git commit](#git-commit)**
        - **[git fetch](#git-fetch)**
        - **[git pull](#git-pull)**
        - **[git push](#git-push)**
        - **[git branch](#git-branch)**
        - **[git checkout](#git-checkout)**
        - **[.gitignore](#gitignore)**
- **[Sample Git Project](#sample-git-project)**
    - **[GitHub Desktop](#github-desktop)**
    - **[Git On the CLI](#git-on-the-cli)**
    - **[Project](#project)**

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

While other VCSs exist, Git is the de facto standard for version control. [This XKCD comic](https://xkcd.com/1597/) captures Git’s reputation

<div align="center">
<img src="https://imgs.xkcd.com/comics/git.png" alt="XKCD comic">
</div>

The above was sourced from [The Missing Semester of Your CS Education](https://missing.csail.mit.edu/2020/version-control/).

### Git vs. GitHub

Before we begin, it is important to separate **Git** and **GitHub** from one another.

- [Git](https://git-scm.com/) is a free and open source VCS created by [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds).

- [GitHub](https://github.com/) is a Git repository hosting service that uses Git under the hood. Beyond just hosting Git repositories, GitHub also adds the following:

    - a pretty Web UI
    - *forking* (copying someone's repository)
    - *pull requests* (requesting a change to someone's repository)
    - *merging* (approving a pull request)
    - other ancillary services like project boards, wikis, issues, CI/CD (GitHub Actions), etc

Before GitHub, if you wanted to contribute to someone else's repository you had to download it, make your changes, and email them to the maintainer who could merge them into their upstream copy. With GitHub, changes can be submitted, discussed, and collaborated on in a public, trackable manner.

The important thing to remember is that **Git is not the same as GitHub**, and GitHub is just one of many [Git hosting providers](https://itsfoss.com/github-alternatives/).

---

## Using Git

### What is a Git Repository?

A Git repository is a folder containing all of the files pertaining to a project. Generally, the idea is that Git tracks the version history of every file in that folder (excluding those specified in a `.gitignore` - this will come later). The data of a Git repository is stored in a subfolder named `.git` in the repository folder.

A Git repository can either exist solely locally (on your computer) or it can have a remote. A remote repository is version of the project that is hosted on the internet. By having a remote (an example being a repository on GitHub) multiple people working on a repository can agree on a common version of that repository. In most cases, everyone working on a project uses the same remote. The basic workflow is as follows:

1. Create a repository locally
2. Sync that repository to a remote
3. Other people download copies of the repository
4. Everyone makes changes
5. Changes get pushed to the remote and conflicts get resolved either automatically or manually

Conflicts usually are mitigated through several strategies, but that is beyond the scope of this guide. Simply put, most conflicts can be resolved by having people push their changes to the remote at different times and having different copies of the remote (called branches) that people can work on separately until it is time to merge those changes into the base version of the repository.

### Git Commands

The following are the most commonly used commands in Git. The term 'commands' is used because Git is traditionally a command line tool; instead of clicking a button to create a repository a programmer would type `git init`. However, this tutorial covers using Git with GitHub Desktop, a GUI for Git. As such, the names of the textual commands will be used, but their meanings will also be explained so they make sense with any way of interacting with Git.

#### git init

**CLI:** `git init`

**GitHub Desktop:** `File > New Repository` *or* `Ctrl + N`

**What does it do?**
The `git init` command reates a new repository in the current directory (or directory specified in the GitHub Desktop GUI). Essentially, all that is happening is a `.git` directory is created and put in the directory specified. The existing files in the directory are not affected.

#### git clone

**CLI:** `git clone <repo>`

**GitHub Desktop:** `File > Clone Repository` *or* `Ctrl + Shift + O`

**What does it do?**
The `git clone` command is primarily used to point to an existing repo and make a clone or copy of that repo at in a new directory, at another location. The original repository can be located on the local filesystem or on remote machine accessible by supported protocols. The `git clone` command copies an existing Git repository.

#### git add

**CLI:** `git add <pathspec>`

**GitHub Desktop:** Under the Changes tab, select the checkbox next to a changed file

**What does it do?**
The `git add` command adds a change in the working directory to the staging area. It tells Git that you want to include updates to a particular file in the next commit. However, `git add` doesn't really affect the repository in any significant way—changes are not actually recorded until you run `git commit`.

#### git commit

**CLI:** `git commit`

**GitHub Desktop:** At the bottom left of the screen, click `Commit to <branch>`

**What does it do?**
The `git commit` command captures a snapshot of the project's currently staged changes. Committed snapshots can be thought of as “safe” versions of a project—Git will never change them unless you explicitly ask it to. Prior to the execution of `git commit`, The `git add` command is used to promote or 'stage' changes to the project that will be stored in a commit. These two commands `git commit` and `git add` are two of the most frequently used.

#### git fetch

**CLI:** `git fetch`

**GitHub Desktop:** On the panel right below the top of the screen, click `Fetch Origin`

**What does it do?**
The `git fetch` command downloads commits, files, and refs from a remote repository into your local repo. Basically, it retrieves the latest changes from a remote without changing the local copy.

#### git pull

**CLI:** `git pull`

**GitHub Desktop:** On the panel right below the top of the screen, after fetching click `Pull Origin` *or* `Repository > Pull` *or* `Ctrl + Shift + P`

**What does it do?**
The `git pull` command is used to fetch and download content from a remote repository and immediately update the local repository to match that content.

#### git push

**CLI:** `git push`

**GitHub Desktop:** On the panel right below the top of the screen, after making local commits click `Push Origin` *or* `Repository > Push` *or* `Ctrl + P`

**What does it do?**
The `git push` command is used to upload local repository content to a remote repository. Pushing is how you transfer commits from your local repository to a remote repo.

#### git branch

**CLI:** `git branch <new branch>`

**GitHub Desktop:** `Branch > New Branch` *or* `Ctrl + Shift + N`

**What does it do?**
A branch represents an independent line of development. Branches serve as an abstraction for the edit/stage/commit process. You can think of them as a way to request a brand new working directory, staging area, and project history. New commits are recorded in the history for the current branch, which results in a fork in the history of the project.
The `git branch` command lets you create, list, rename, and delete branches.

#### git checkout

**CLI:** `git checkout <branch>`

**GitHub Desktop:** `Current branch > <the branch you want to view>`

**What does it do?**
The git checkout command lets you navigate between the branches created by git branch. Checking out a branch updates the files in the working directory to match the version stored in that branch, and it tells Git to record all new commits on that branch. Think of it as a way to select which line of development you’re working on.

#### .gitignore

Ignored files are tracked in a special file named `.gitignore` that is checked in at the root of your repository. There is no explicit git ignore command: instead the `.gitignore` file must be edited and committed by hand when you have new files that you wish to ignore. `.gitignore` files contain patterns that are matched against file names in your repository to determine whether or not they should be ignored. In short, **you can list the names of files you don't want tracked in the `.gitignore` file.**

The Git command descriptions above were sourced from [Learn Git with Bitbucket Cloud](https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud).

---

## Sample Git Project

### GitHub Desktop

The fact that this guide has an option to use GitHub Desktop is noted several times above, without being explained much further. GitHub Desktop is an open source Git client designed by GitHub. Before continuing, it is very important to understand that GitHub Desktop is primarily designed to work with GitHub. In GitHub's [explanation of Desktop](https://github.com/desktop/desktop/blob/development/docs/process/what-is-desktop.md), they say the following:

> It is intended primarily to extend the features of GitHub, not to be an agnostic Git client or replicate the feature set of github.com. While we support very basic functionality that will allow the app to function with other hosting providers, we prioritize work that allows the end-to-end GitHub and GitHub Enterprise experience to shine and takes advantage of the fact that we can closely integrate with GitHub features.

In other words, GitHub Desktop is mostly suitable as a beginner tool, and moving beyond the functionality described in this tutorial should be done with either a hosting provider agnostic Git GUI or the Git CLI.

### Git on the CLI

First, see [here](https://learntocodewith.me/getting-started/topics/command-line/#h-what-is-the-command-line) for an explanation of the CLI.

> When you use programs with Graphical User Interfaces (GUI) certain buttons perform certain tasks on the computers. The Command Line Interface does that too, but it allows you to do it with more precision and power. You type words and hit enter, the shell interprets those words, and works with the OS kernel and files to execute the command.

If you are interested in learning Git to do serious programming, you should learn the Git CLI rather than a Git GUI like GitHub Desktop. 
There are several reasons for this:

- **GUIs are fickle.**  The original Git CLI was created in 2005 and has endured for over 15 years without significant changes. If you learn it, there's a decent chance that it won't go away within your lifetime. GUIs will continuously change or stop being developed.
- **GUIs hobble you.** GUIs all differ greatly in capabilities and usage. However, they all lack the ability to be integrated into scripts and be customized to your liking. Some (like GitHub Desktop) even lack important security features like [signing commits and tags](https://github.community/t/github-desktop-doesnt-work-with-gpg-signing-commits/171395).
- **Everybody uses the CLI.** If you have to work on a coworker's machine, a headless server, or an embedded device (such as a Raspberry Pi), the CLI will be there, and it will be identical to the CLI on your machine. You won't skip a beat.

### Project

In this sample project, you'll fork this repository, clone it to your machine, create a new branch, make a change, commit that change, push the change, and finally make a pull request into the master branch of the main repository. 
It's just an example of the basic Git workflow described in [What is a Git Repository?](#what-is-a-git-repository).

#### Prerequisites

- [GitHub Account](https://github.com/join)
- Git
    - [GitHub Desktop](https://desktop.github.com)
    - [Git for Windows](https://gitforwindows.org) (recommended if you are on Windows)
    - [Vanilla Git](https://git-scm.com/downloads)

#### Steps

1. Fork the repository

    Go to this repository's [home page](https://github.com/not-stirred/learn-git) and on the upper right corner click `Fork`.

2. Clone the repository

    Clone this repository by selecting `URL` in the pop up window and entering `<mygithubusername>/learn-git`.

    ***or***

    ```shell
    git clone https://github.com/<mygithubusername>/learn-git
    ```

3. Create a new branch

    Create a new branch named `<mygithubusernamename-contributed>` and select the option `Publish your branch`.

    ***or***

    ```shell
    # Option 1
    git branch <mygithubusername-contributed>
    git checkout <mygithubusername-contributed>

    # Option 2
    git checkout -b <mygithubusername-contributed>
    ```

4. Make your change

    Create a new file called `<mygithubusername>-contributed.txt` in the `contributors` directory and add a message.

5. Commit your change

    Now, on the left side of GitHub Desktop, you should see `1 changed file` above the path to the new file. Under that, title your commit, optionally add a description, and click `Commit to <mygithubusername-contributed>`.

    ***or***

    ```shell
    git add .
    git commit -m "<your commit title>"
    ```

6. Push your change

    You should see a prompt that says `Push commits to the origin remote`. Either click the button labelled `Push origin` next to it or push some other way.

    ***or***

    ```shell
    git push
    ```

7. Create a pull request

    Now you have your own version of the learn-git repository, but you need to merge your changes from the head repository (your fork) to the base repository (not-stirred/learn-git). GitHub Desktop has a handy way to do this by just clicking `Create Pull Request`. Once you do so it will take you to the GitHub website, where you can title, describe, and file your PR.

---

Congratulations! You now have a basic understanding of Git. Keep in mind that GitHub Desktop is not a tool oriented towards more advanced workflows, and if you find yourself being limited by it your best option is to learn the Git CLI. Some of the best resources for doing so are the free [Pro Git](https://git-scm.com/book/en/v2) book hosted on git-scm.com and [Learn Git with Bitbucket Cloud](https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud) by Atlassian.

If you liked this tutorial please star the repository!
