# Git

This is a quick reference guide to using common Git commands in your terminal.

---------------
<br><br>

### Create a Git Repo
Running the following command will create a .git folder to start storing your repository in. This command only creates the local repo, not a remotely hosted repo. 
```cmd
git init
```
<br>

### Add File / Changes to Repo
Add new files or add changes from already tracked files to the repo. Once you have added your files, you can commit them to the repo using the “git commit” command. 
```cmd
git add file.name  // Adds a single file named file.name
git add *          // Recursively add all files and folders
```
<br>

### Remove Staged File / Undo Add File
Remove a file after you have added it to the current commit. 
```cmd
git reset filename.txt
```
<br>

### Commit Changes To The Repo
Use the following command to commit your changes to the repo.
```cmd
git commit 
```
<br>

### Clone a Repo
Use the following command along with a URL pointing to a hosted repo to clone a copy of the repo on your local machine. 
```cmd
git clone https://github.com/docker-library/wordpress
```
<br>

### Get Branch Status
Use the following command to see what the status is of your current branch. The status will show uncommitted and added changes. 
```cmd
git status
```
<br>

### Get Branch Details
Use the following command to see what the status is of your current branch. The status will show uncommitted and added changes. 
```cmd
git status
```
<br>

### Checkout Branch
Checkout a specific branch. You can also use this to reset all changes by checking out the current branch. 
```cmd
git checkout branch-name
```
<br>

### Push Changes
Push your changes back to the hosted repo. 
```cmd
git push origin branch-name
```
<br>

### Compare File Difference
Compare the differences between the repo version of a file and your current changes. 
```cmd
git diff file.name
```
<br>

### Create A New Branch
Create a new branch from the current branch you are working on. In most cases, you'll want to switch to the master or develop branch before creating a new branch. 
```cmd
git checkout -b [name_of_your_new_branch]
```
<br>

### Show All Branches
Show all of the branches in the repository. 
```cmd
git branch -a
```
<br>

### Resync with Master Branch
Completely resync your working directory with the master branch. 
```cmd
git fetch origin && git reset --hard origin/master && git clean -f -d
```
<br>

### Visualize Branches
Get a visual look at your branches with the following command. Use ```q``` to quit.
```cmd
git log --graph --oneline --branches
```
<br>

```cmd
git log --graph --full-history --all --pretty=format:"%h%x09%d%x20%s"
```
<br>

### Do Not Track File Permissions
The following commands will allow you to no longer track the file permissions on your files. For a detailed instructions, [see the guide here](https://medium.com/@tahteche/how-git-treats-changes-in-file-permissions-f71874ca239d).

First, check if the tracking is turned on in your repo
```shell
git config --get --local  core.filemode
```

If you would like to disable it, run the following command from the root of the repo.
```shell
git config --local core.fileMode false
```
