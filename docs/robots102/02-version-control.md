# Git and Version Control

This lesson will take you through Version Control Systems, Git, GitHub, and generally how code is managed in bigger projects.

## What is Version Control?

Have you ever had a project end up looking something like this at the end of development?

- `Project`
- `Project (1)`
- `Project (2)`
- `Project (3)`
- `Project FINAL`
- `Project FINAL take two`
- `Project FINAL ACTUALLY`
- `Project FINAL (broken)`
- `Project FINAL WORKING AGAIN`
- `Project SUBMITTED`

This is a primitive form of version control - taking "regular" backups at certain points in development.
However, this is messy and unsustainable.
Imagine what that sort of pattern looks like when rather than a single folder or document, you have potentially hundreds of files that a whole team of people are trying to edit!

A _Version Control System_ (VCS) is the solution to this.
The two most common implementations that you're likely to encounter are Git and Subversion (better known as SVN), but they have many overlapping concepts.
This lesson will focus on Git, but most of this content is also applicable to SVN [^svn].
Put simply, a VCS stores the state of your workspace at various fixed points called _commmits_ by tracking the _differences_ between those versions.
You can then _push_ changes to a _remote_ server, and later _pull_ those changes on a different computer to synchronise the changes.

[^svn]: The most common client implementation of SVN you're likely to encounter, at least on Windows, is [TortoiseSVN](https://tortoisesvn.net/).

## Prerequisites

Before digging into the main lesson, you'll need to install Git and sign up for a GitHub account.

### Git

Download and install git from [here](https://git-scm.com/install/).
If you're on Windows, you can optionally run `winget install Git.Git` in a terminal instead if you just want it installed with all the defaults.

### GitHub

GitHub is a platform which provides Git repository hosting.
To play with the remote features Git provides, you'll need to sign up with GitHub so you can make your own repositories.
Do so [here](https://github.com/signup) - we recommend signing up with your email and a username rather than signing in with any linked services.

We also _strongly_ recommend you install the [GitHub CLI](https://cli.github.com/), as this will make setting up Git much easier later.

## Getting Started

### Configuring Git

Before you can make any commits, however, Git needs to know who you are.
To start with, run:

```shell
git config --global user.name "YOUR NAME HERE"
```

Whatever you provide to Git should match the display name you've given to GitHub in your account setup.
Git also needs your email.
If you're OK with it being semi-publicly accessible, you can use your actual email that you signed up to GitHub with here.
However, if you would prefer to keep it private, go to your GitHub account email settings [here](https://github.com/settings/emails), and:
1. Turn on "Keep my email addresses private" and copy the email address it gives you in this box for later.
2. Optionally, check "Block command line pushes that expose my email" as well.

If you've done that, you can now tell git your email:

```shell
git config --global user.name "email GitHub gave you here"
```

If you turned on using a private email address, use that here, otherwise use the primary address for your account.

At this point, Git knows who you are, but GitHub doesn't! (Locally, anyway.)
This is where installing the GitHub CLI is important, as it can _configure_ Git with the required credentials to interact with your repositories.
To do so, run the following in a terminal and follow the instructions:
```shell
gh auth login -w -p https
```

At this point, you're all ready to go!
However, we recommend changing the following configuration for quality of life at this point:

```shell
git config --global push.autosetupremote true
git config --global pull.rebase false
```

### Terminology

- **Git** is a version control system (VCS) that is used for tracking changes in files. It is a local system that can interface with external systems (remote repositories).
- A **repository** (or _repo_) is a single "project" tracked with a VCS, containing a collection of files and folders and a set of commits.
- A **remote** is a separate, remotely accessible repository which provides a central location for code to be shared and changes to be synchronised between devices. 
- **GitHub** is a _remote_ repository host. It also provides additional functionality in the form of *pull requests* (PRs) and *CI/CD* functionality.
- The **main** branch or just `main` is the "default" branch for code to live on, and should usually be considered the "current" state of any project. Previously named `master`.
- **Branches**: Each branch is an independent series of commits tracking changes from a certain point in time. Think of branches like a tree, the main branch is the trunk (where everything stems from) and each branch is, well, a branch. Each branch can develop code independently from everything else, allowing changes, testing, and development to happen without breaking production.
- A **commit** in its simplest form is a set of changes. It consists of the files which have been added, modified, or deleted, along with a message describing what it has changed. The repository is made up of commits, which git tracks.

For more details and further terminology see [the Git docs](https://git-scm.com/docs/gitglossary).

### Operations

- **Cloning** is the first-time download of a new repository's data and version control information.
- **Staging**: Selecting the changes which you want to be in the next commit.
- **Committing** means saving a set of changes and a message into a _commit_, which then gets added to your current _branch_.
- **Push**: When you make a commit, it is a local commit and only present on your device. The same applies to any new branches created. A push is when you upload those commits and potentially branches to a _remote repository,_ often on GitHub.
- **Pull**: When changes are made to the remote repository, you must _pull_ the changes to update your local repository.
- **Merging**: Combining the changes from two different _branches_ into a single branch.

## Demonstrations!

github requires setting a display name to start with
**linux basics should be lesson 01**
full name of vscode
vscode installation
go over cd/pwd/terminal/cmd:
%userprofile%
macos installation instructions (homebrew)
git init -> initialise
explain staging better
have a messed up repo as an example?

- Setting up a new repo on GitHub
- Making a commit

## Extra Resources

Below are some very useful resources if you're confused or want to further your learning.
Learn Git Branching is an interactive, graphical teaching tool which takes you through the basics of how Git works.
Alternatively, the official Git and GitHub documentation cover many uses beyond what's covered here, as well as providing the same content in a different form.

- [Learn Git Branching](https://learngitbranching.js.org/)
- [Git documentation](https://git-scm.com/docs/gittutorial)
- [GitHub documentation](https://docs.github.com/en/get-started/using-github/hello-world)

## Making Git Fancy

The default git diff output _works_, but it's nothing fancy. If you want a nice display, [delta](https://dandavison.github.io/delta/) is an excellent option with quite a lot of nice features.