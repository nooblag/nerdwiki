## Making a new repo

`mkdir newrepo`

`cd newrepo`

`git init`

`touch README.md`

`git add .` (to add all files in directory to index)

`git commit -m 'Initial commit.'`

## Branches

Checking out a new branch

`git checkout -b development`

## Add files, then commit changes -

`git add .`

`git commit -m 'Added files to development branch.'`

## List all branches with -

`git branch`

## Change branches with -

`git checkout master` (or whatever branch you want)

## Merge branches (this example is merging development branch with master branch, make sure you've checked out the master branch first) -

`git merge development`

## Cloning a repo from remote server

Make sure you've checked out another branch on the remote serverthat isn't the master branch, say a development branch, otherwise you'll get an error.

`git clone ssh://user@loe.org:/git/repo nameofbranch`

## Make changes, then push back to server -

`git add .`

`git commit -m "Made changes"`

`git push`

Or you could rsync all files between servers, then init a git repo in the directory holding the files. Then use the following to push any changes to a new branch on the remote server -

`git push user@loe.org:/git/repo -b newbranch`

## Undo unstaged changes to files -

`git checkout .`

## Errors and workarounds

`branch checked out` error is common when trying to push to a remote server, just make sure that the branch you're trying to push to isn't already checked out on the remote server. Use git checkout anotherbranch on remote server to switch to another branch.

## GitHub

Small section on making a new repo on GitHub and pushing to it from a local repo.

First ensure git variables on local machine match GitHub username and email -

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

## Add new files and auto rm deleted files from staging

`git add -A`

or

`git add -u`

## To edit and sort

`git bundle create some file HEAD`

`git diff 1b6d > my.patch`

`git apply < my.patch`

`git reset --hard`: load an old save and delete all saved games newer than the one just loaded.

`git checkout 93b1`

`git revert 93b1` - reverts to commit and updates commit message with revert info. 
