## Creating a new repository

`mkdir newrepo`

`cd newrepo`

`git init`

`touch README.md`

`git add .` (to add all files in current directory to index)

`git commit -m 'Initial commit.'`

## Branching

### Check out a new branch

`git checkout -b develop`

Add all files, then commit changes -

`git add .`

`git commit -m 'Added files to develop branch.'`

### List all branches

`git branch`

### Change branches

`git checkout NAME_OF_BRANCH`

### Delete branch

`git branch -d NAME_OF_BRANCH`

### Delete remote branch

`git push origin --delete NAME_OF_BRANCH`

## Merging

Merge branches (this example merges `develop` branch with the current working branch) -

`git merge develop`

### Squash

Merge a branch as one commit.

Working on example branch `develop`

`git checkout master`

`git merge --squash develop`

This will present editor to allow you to enter a commit message that includes all commit messages for the `develop` branch -

`git commit`

Or, this will just use your commit message without the messages from `develop` branch -

`git commit -m "Your commit message"`

## Cloning

`git clone ssh://user@server.org:/git/repository NAME_OF_BRANCH`

### Make changes, then push back to server

`git add .`

`git commit -m "Made changes"`

`git push`

## Log

### Print past commits

`git log`

### Print a single line for each past commit

`git log --pretty=oneline`

## Checkout specific commit

### Example workflow

Use `git log` to find a specific commit -

	commit ba6af9e85675a974917a86488bc81fcd3252d1a8
	Author: jl <jl@leagueofevil.org>
	Date:   Mon Oct 31 23:09:28 2011 +1100

	    Added Irssi.

To checkout that commit, `checkout` using the commit hash -

`git checkout ba6af9e85675a974917a86488bc81fcd3252d1a8`

Or just using the first 4 characters (or however many characters you want) -

`git checkout ba6a`

## `assume-unchanged`

### Mark a file so git will temporarily ignore changes to it

`git update-index --assume-unchanged nameOfFile.txt`

### Undo

`git update-index --no-assume-unchanged nameOfFile.txt`

### List marked files. Those that are prefixed with a lowercase `h` are marked as `assume-unchanged`

`git ls-files -v`

### Or, use this to list only those marked as `assume-unchanged`

`git ls-files -v | grep "^[[:lower:]]"`

## Stashing

### Save the changes you have made without commiting them

`git stash`

### List of your stash

`git stash list`

### Bring back most recent stash to current branch

`git stash apply`

### Bring back a specific stash

`git stash apply @{2}`

### Bring back the most recent stash and immediately `drop` the stash

`git stash pop`

### Drop specific stash

`git stash drop stash@{2}`

## Misc commands

### Undo unstaged changes to files

`git checkout .`

### Add new files and auto `rm` deleted files from staging

`git add -A`

or

`git add -u`

### Revert to a specific commit and update commit message with info about the revert

`git revert 93b1`

### Misc - to edit and sort

`git bundle create some file HEAD`

`git diff 1b6d > my.patch`

`git apply < my.patch`

`git reset --hard`

## GitHub

Small section on making a new repo on GitHub and pushing to it from a local repo.

First ensure correct SSH pubkeys are setup on GitHub and on your local machine.

Ensure git variables on local machine match GitHub username and email -

`git config --global user.name "username"`

`git config --global user.email user@domain.org`

`git config --global github.user username`

`git config --global github.token 0123456789yourf0123456789token` (if you need API access)

Then create a new local repo -

`cd /newrepo`

`git init`

`touch README.md`

`git add .`

`git commit -m "Initial commit."`

Then create a new repo on GitHub.

After repo is made, set local repo to push to GitHub repo -

`git remote add origin git@github.com:Your-Username/awesomeProject.git`

To push to GitHub from local machine -

`git push -u origin master`

## Setting up a git server

Using gitolite and Debian.

NOTE: Does not work with Dropbear. Use OpenSSH Server.

Make sure git is installed with `aptitude install git git-core`.

Add user for gitolite -

`sudo adduser git`

Change to new user -

`su git`

Download gitolite source -

`git clone git://github.com/sitaramc/gitolite`

Install gitolite -

`gitolite/src/gl-system-install`

Add bin to PATH in ~/.bashrc (or similar) -

`PATH=/home/git/bin:$PATH`

Setup with public key -

`gl-setup ~/nameofkey.pub`

On client workstation (not the server), clone gitolite-admin to add users and repos -

`git clone git@server:gitolite-admin`

Add new keys to `gitolite-admin/keydir`. Edit `gitolite-admin/conf/gitolite.conf` to add new repos. Commit and push to server to apply changes.
