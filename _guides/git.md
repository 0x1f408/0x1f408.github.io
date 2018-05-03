---
layout: post
permalink: /guide/git/
title: Version Control Systems & Git
subtitle: Quick overview of Version Control Systems and creating your first project on Git
---

<!-- todo: refactor this for this project -->
# Revature-Tantalum
### Business Process Management application for a large-scale metal distributor

Project repositories located at [GitLab](https://gitlab.com/tantalum/).

* [Database design documentation](https://gitlab.com/tantalum/database-design)

* [Main project files](https://gitlab.com/tantalum/tantalum-main)

* [Test data generator](https://gitlab.com/tantalum/testdata)

### Getting started: GitLab

#### 1. Create an account at [GitLab](https://gitlab.com/). 
You've already done this. By default, project members will have role 'Developer,' which
will allow you full read/write access to project files.

#### 2. Download & install Git.
This is what will actually let you read/write to GitLab.

* **Windows**: Download [Git For Windows](https://gitforwindows.org).

* **\*Nix**: Download Git via apt/yum: `apt-get install git`

#### 2. Generate an SSH key.
You will need to do this to be able to write to GitLab. On Windows, `ssh-keygen` is
installed alongside Git, or included with OpenSSH on \*Nix.

1. Run `ssh-keygen`.

* On Windows, you may need to run this from Git Bash, depending on your installation
settings.

2. Set a passphrase and save private key to `C:/Users/%NAME%/.ssh/id_rsa`

3. Generate a public key and save it to `C:/Usrs/%NAME%/.ssh/id_rsa.pub`.

4. Copy public key. This should be `ssh-rsa <1024-4096 digit key> <nick@device>`.

5. Make sure you copied the **public** key.

#### 3. Save SSH key to GitLab

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