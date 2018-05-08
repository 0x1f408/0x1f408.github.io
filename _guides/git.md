---
layout: post
permalink: /guide/git/
title: Version Control Systems & Git
subtitle: Quick overview of Version Control Systems and creating your first project on Git
---
## 0x1f408.me
<!-- todo: refactor this for this project -->

### Basics of Version Control Systems

#### What

#### Why

### Getting started: GitHub

#### 1. Create an account at [GitHub](https://github.com).

#### 2. Download & install Git.
This is what will actually let you read/write to GitHub.

* **Windows**: Download [Git For Windows](https://gitforwindows.org).

* **\*Nix**: Download Git via aptitude (or package manager of your choice): `apt-get install git`

#### 2. Generate an SSH key.
While not required, this greatly simplifies interacting with GitHub. On Windows, `ssh-keygen` is
installed alongside Git, or included with OpenSSH on \*Nix.

1. Run `ssh-keygen`.

* On Windows, you may need to run this from Git Bash, depending on your installation
settings.

*For the below, `~` is used as a shortcut for your home directory*:

  * **Windows**: `%USERPROFILE%`, or `C:\Users\%USER%\`
  
  * **Linux**: `~` or `/home/$USER/`
    
2. Set a passphrase and save private key to `~/.ssh/id_rsa`

3. Generate a public key and save it to `~/.ssh/id_rsa.pub`.

4. Copy public key. This should be `ssh-rsa <1024-4096 digit key> <nick@device>`.

5. Make sure you copied the **public** key (and not the private).

#### 3. Save SSH key to GitHub

1. Open GitLab.

2. Click your profile icon (top right corner).

3. Select `Settings` from the dropdown menu.

4. Select `SSH Keys` from the left menu.

5. Paste your copied **public** key into the field at right.

6. Assign your key a name. username@hostname is recommended.

7. Select `Add Key`.

### Getting started: Git

#### 1. Open Git

1. Set your desired $NAME: `git config --global user.name="$NAME"`.

2. Set your desired $EMAIL: `git config --global user.email="$EMAIL"`.

3. View global config with `git config --global --list`.

Note that the `$NAME` and `$EMAIL` will be attached to every commit you make,
i.e.: viewable by anyone with read access to the repository.

#### 2. Clone project

1. Create a folder to copy projects into. Personally, I use `%HOME%/Documents/dev`.

2. Navigate into that folder.

3. Open Git Bash, enter `git clone` and the repository address. This is visible on the project
page on GitLab, and should be something like

* HTTPS: `https://gitlab.com/tantalum/revature-tantalum.git`

* SSH: `git@gitlab.com:tantalum/revature-tantalum.git` 

4. Your full command should be something like `git clone git@gitlab.com/tantalum/revature-tantalum.git`.

#### 3. Add changes & commit

1. After modifying project, run `git add .` in the project directory to add all files. If you're
generating any log or editor files:

  1. Create a file named `.gitignore`.

  2. Specify all files and extensions to ignore in that file, one per line.

2. Run `git commit -m "commit message"` to commit (stage) changes. "Commit message" should be
a brief description of what was changed, in imperative tense. [This](https://chris.beams.io/posts/git-commit) 
is a thorough guide to writing useful commit messages; read it.

3. Define your origin with `git remote add origin $REPOSITORY`, where $REPOSITORY is the address you used to 
`clone` the project.

4. Push the changes to the remote repository (GitLab) with `git push -u origin master`.
_Note: You should be able to write to the `master` branch, contact me if otherwise._