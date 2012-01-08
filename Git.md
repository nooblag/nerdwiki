## Creating a new repo

`mkdir newrepo`

`cd newrepo`

`git init`

`touch README.md`

`git add .` (to add all files in directory to index)

`git commit -m 'Initial commit.'`

## Branches

### Checking out a new branch -

`git checkout -b development`

### Add all files, then commit changes -

`git add .`

`git commit -m 'Added files to development branch.'`

### List all branches with -

`git branch`

### Change branches with -

`git checkout master` (or whatever branch you want)

## Merging

Merge branches (this example is merging development branch with master branch, make sure you've checked out the master branch first) -

`git merge development`

## Cloning a repo from remote server

Make sure you've checked out another branch on the remote server that isn't the master branch, say a development branch, otherwise you'll get an error.

**NOTE:** This dosen't matter if cloning a bare repo.

`git clone ssh://user@loe.org:/git/repo nameofbranch`

### Make changes, then push back to server -

`git add .`

`git commit -m "Made changes"`

`git push`

Or you could rsync all files between servers, then init a git repo in the directory holding the files. Then use the following to push any changes to a new branch on the remote server -

`git push user@loe.org:/git/repo -b newbranch`

## Git log

`git log`

Lists all commits and commit messages. The first 4 characters of a commit hash allow you to identify and work with specific commits.

### Example workflow

Use `git log` to find a specific commit -

	commit ba6af9e85675a974917a86488bc81fcd3252d1a8
	Author: jl <jl@leagueofevil.org>
	Date:   Mon Oct 31 23:09:28 2011 +1100

	    Added Irssi.

To checkout that commit, use the first 4 characters of the commit hash -

`git checkout ba6a`

## Misc commands

### Undo unstaged changes to files -

`git checkout .`

### Add new files and auto rm deleted files from staging -

`git add -A`

or

`git add -u`

### Revert to a specific commit and update commit message with info about the revert -

`git revert 93b1`

### To edit and sort and document -

`git bundle create some file HEAD`

`git diff 1b6d > my.patch`

`git apply < my.patch`

`git reset --hard`: load an old save and delete all saved games newer than the one just loaded.

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

To push to GitHub from local machine, enter the following command -

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

Clone gitolite-admin to add users and repos -

`git clone git@server:gitolite-admin`

Add new keys to `gitolite-admin/keydir`. Edit `gitolite-admin/conf/gitolite.conf` to add new repos. Commit and push to server to apply changes.
