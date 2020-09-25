# Master Git
## Git Installation
Download and install the up-to-date version of Git on your desktop from [Git website](https://git-scm.com/download/win)

-----------------

## SSH Authentication
1. check your current folder path
```sh
$ pwd
```
2. check if .ssh folder exits
```sh
$ .ssh
```
3. create .ssh folder
```sh
$ mkdir .ssh
```
4. direct to .ssh folder
```sh
$ cd .ssh/
```
5. generate SSH key
```sh
$ ssh-keygen -t rsa -C "youremail@gmail.com" 
```
- Press Enter when message *Enter file in which to save the key* shows up
- Enter your choosen password when message *Enter passphrase* shows up or Press Enter to skip setting up password. Please mind that your typed letters would show on screen. Just click enter when finished typing in password. 
- Reenter your choosen password when message *Enter same passphrase again* shows up

6. check the files generated, should have id_rsa and id_rsa.pub 
```sh
$ ls -al
```
7. open id_rsa.pub file with your editor, here notepad++ is used
```sh
$ notepad id_rsa.pub
```
8. copy all everything in id_rsa.pub file to clipboard
9. Add SSH Key in your github or other git version control app
    - Go to github or your git version control app website account setting
    - click SSH Key 
    - Add New Key and paste everything in id_rsa.pub
10. SSH key is added
11. Test SSH key connection

------------
## Git Basics
### Gitting Started/New Repo

- check the current file path, create a new folder *projects*, update the file path to *projects*
```sh
$ pwd
$ mkdir projects
$ cd projects/
```
- create a git repo or working folder *demo* in *projects* folder by git
```sh
$ git init demo
```
- check if *demo* repo is created under *projects*
```sh
$ ls 
```
- change path to *demo* after comfirming *demo* repo is created
```sh
$ cd demo
$ ls -al
```
now *(master)* shows up with your path indicating current at the *master* branch

### Git States
There are three states related to the files being managed by Git: 
1. Working Directory
    - contains all the files and folders related for your application

2. Staging Area
    - Between working directory and repository, staging area is used to prepare for the next commit. 

3. Repository (.git folder)
    - contains all the committed or saved changes to the Git repository. (Git's history)

4. Remote state (the repo state on remote server)

check the status of the current git repo
```sh
$ git status
```

### File Operations
- create folder

- create a file, for example create a README.md file with notepad++
```sh
$ notepad README.md
```

- check the repo git status after add README.md file
```sh
$ git status
```

It shows files to commit

- add the uncommitted README.md file then the repo enters the staging area
```sh
$ git add README.md
```

- commit the added README.md file in staging area with a commit message in double quote markers
```sh
$ git commit -m "commit message"
```

### Git repo folder *.git* folder 
The *.git* folder can be removed from the git repo folder. The consequence is the folder is no longer a git repo as indicated by *(master)* disappearing from the path
```sh
$ rm -rf .git
```

When check the current folder git status after remove .git, it shows it is no longer under version control
```sh
$ git status
```

To place the current folder under version control, use git init command. "." means current folder
```sh
$ git init . 
```

Check the status of the current folder whether under version control or not
```sh
$ git status
```

### Commits and Messages

- add all files in the current folder to staging area with "."
```sh
$ git add .
```

- commit the files in staging area git repository
```sh
$ git commit
```

without the *-m "mymessage"* commit message identified, a core editor with pop up to configure the git commit messages


### Commit details and Git Log
- Find out the git commit history
```sh
$ git log

```

- git show to show history
```sh
$ git show
```

press q to quit form the git show message

- get files that Git is tracking
```sh
$ git ls-files
```

- add a new file to the current folder
```sh
$ touch new.file
```

- removew a file form current folder
```sh
$ rm new.file
```

### Express Git commit: add and commit together
```sh
$ git commit -am "CommitMessage"
```
### Backout changes
first change a file content in the current repo folder
- check the status of the git repo
```sh
$ git status
```

- add the change to staging area
```sh
$ git add .
```

-- move the file out from the staging area
```sh
$ git reset HEAD README.md
```

The README.md file is still changed but is no longer in the staging area.

- Remove the changes in README.md file
```sh
$ git checktout -- README.md
```

### History and Making new commands with Alias
```sh
$ git help log
```
- get a simplified version of log history
```sh
$ git log --oneline --graph --decorate --all
```

- create a git alias for the long *$ git log --oneline --graph --decorate --all* command
```sh
$ git config --global alias.hist "log --oneline --graph --decorate --all"
```

- list git config entries
```sh
$ git config --global --list
```

- test git hist alias
```sh
$ git hist
```

- git alias command can be used with args

```sh
$ git hist --README.md
```

To show git history related to README.md only


### Rename and Delete File after add files to .git repository stage (after add and commit)
```sh
$ git mv example.txt newName.txt
$ git commit -m "updata file name"
```

```sh
$ git rm newName.txt
$ git commit -m "delete newName.txt"
```


### Rename and delete files outside .git repository
- remove files in the current folder with bash command not git command

```sh
$ touch newfile.txt
$ mv newfile.txt newName.txt
$ rm newfile.txt
```
- git add -u will pick up the changes make with git command, but not the ones outside .git repository
- to pick up all the changes in the current folder, us git add -A with captical 'A'
```sh
$ git add -A
$ git commit -m "commit alll changes"
```


### Ignore files during commit
- use .gitignore and add files to be ignored to the file
- for example: *.log into .gitingore file, then any file with .log with be ignored
```sh
$ notepad .gitignore
$ git add .gitignore
$ git commit -m "Adding ignore file"
```

-------
## Advanded Git 
### Compare differences
- compare difference between two commits
```sh
$ git help diff
$ git hist
$ git diff fij3279 fwei3894
$ git diff fij3279 HEAD
```


HEAD is the last commit pointer

### Branching, Merging and Conflict Resolution
- Branch = timeline of commits
- brach names are labels
- Deletion removes labels only

- type of merges
    - Fast-forward
        - Simplest case
        - Like never branched (commit on destination)
        - Can be disables
    - Automatic merge
        - non conflicting merge detected
        - preserves both timelines
        - merge commit on destination
    - Manual merge
        - resolve conflicts first
- Special markers
    - HEAD, like pointers, last commit of the branch
- check git branches
```sh
$ git branch
```
- create and switch to a new branch
```sh


```

- add and commit on the new branch
```sh
$ git add .
$ git commit -m "Update on newBranch"
```

- check history
```sh
$ git hist
```

- compare difference between branches
```sh
$ git diff master newBranch
```

- after commiting on children branch, switch back to master branch before merge
```sh
$ git checkout master
```
- merge the newBranch with master branch: fast forward merge
```sh
$ git merge  updates
$ git hist
```
Now HEAD master and newBranch point to the same git commit ID

- after merge, the children branch can be deleted
```sh
$ git branch -d newBranch
$ git branch
```

- return back to master and modify the same file at the same position to create the conflicts
```sh
$ git checkout -b very-bad
$ notepad README.md  /* create a change in read me file
$ git commit -am "very bad update"
```


- resolving conflicts before merge
```sh
$  git checkout master 
$ notepad README.md /* modify the readme file at the same position
$ git commit -am "update at master"
```
- check branches before merge
```sh
$ git branch -a
```
- Try auto merge the two branches

```sh
$ git checkout master
$ git merge newBranch
```
Message reads there is conflict

- review the conflicting file
```sh
$ cat README.md
```
- resolve the conflict with mergingtool
```sh
$ git mergetool 
```

- commit after resolving conflicts
```sh
$ git commit -m "resolve commit"
```

- check git status after resolving merge
```sh
$ git status
```
Message read that is a README.md.orig file waiting to be staged. This is the original file of README. Add this .orig file into .gitignore file. Then commit the .gitignore file

```sh
$ git commit -am "update .gitignore"
```


### Git Tags
- create and add a tag to a commit
```sh
$ git tag myTag
$ git tag --list
```
- delete a tag
```sh
$ git tag -d myTag
```
- Better practice with use tag with annotation
```sh
$ git tag -a V1.0 -m "Release 1.0"
$ git tag --list
```
- Show the tag annotation
```sh
$ git show V10
```

### Stashing
- file changed, which should not happen now
- use git stash to undo the changes
```sh
$ notepad README.md /* update the readme file
$ git status /* show README.md should be added
$ git stash /* git update the head pointer
$ git stash list /* shows the stash list
$ git status /* now back to a clean working directory
```
- delete a stash action
```sh
$ notepad LICENSE.txt /* modify the LICENSE txt file
$ git commit -am "update license file" /* commit the LICENSE file change
$ git status /* clean working directory
$ git stash pop /* two actions: apply and drop 
/* stash apply: apply whatever the stash is the last stash, that put the changes back in README file
/* stash drop: it drop the stash that is applied
$ git stash --list /* no stash
$ notepad README.md /* readme.md file all changes are removed
$ git commit -am "update readme again"
$ git status /* clean work directory
```

### Time Travel with Reset and Reflog
- change to a different commit point, eg. roll back to previous point
```sh
$ git hist /* show the history of git commits
$ git reset ce2di90 --soft /* reset the ce2di90 commit
```
- 3 types of reset:
    - soft: change the head pointer, keep all commit
    - mixed: change head pointer, some commits deleted
    - hard: change head pointer, add and commits deleted. clean working directory

- Reflog used to go back to a specific commit id
```sh
$ git reflog /* show all actions 
$ git reset cie1038ji --hard /* reset the head pointer back
$ git log --oneline /* now git history back again
```
-------
## Github
- Link github repo to a local repo
```sh
$ git remote -v /* in the local repo, check if there is connected remote repo
$ git remot add origin githubURL /* add take two args: name of the reference(origin, or any name. by convention, the first and primary remote repo is named origin) and the full URL to the remote repo. 
$ git remote -v /* now the local git repo is connected with remote origin
```
- push local git repo to a newly created github repo
```sh
$ git status /* check status of local repo
$ git remote -v /* check remote repo connection
$ git push -u origin master --tags 
/* snychronize the changes between local git and remote git repo
/* -u tracking branching relationship between local master branch and remote master branch
/* after -u is origin: name of the remote repo going to use, next time push action, -u wont be needed.
/* after name of remote repo is branch going to push up to
/* --tag will send all the tags used in current repo up to github
```
-----
## Github Repository
### Git clone
- create a local copy of remove repo with git clone
```sh
$ cd projects/ /* change the path to the desired folder path
$ git clone repoURL
$ ls -l /* check the folders in the current path. There should be new folder for the cloned repo
$ cd myRepo/ /* update path to myRepo, by default it should show master branch
$ ls -al /* check all the files in myRepo folder
$ git remote -v /* list all the remote repo available
```

- remove the cloned repo folder
```sh
$ cd .. /* change path to the upper folder of the repo folder
$ rm -rf myRepo /* remove myRepo folder
```

- clone a remote github repo to local and define the folder name
```sh
$ git clone nyRepoURL myFolderName 
$ ls -al
```

### Get contect: seed the repository
- copy files to the current local repo folder
- bash command cp
```sh
$ cp -R ~/Downloads/initilizr/* . 
$ git add .
$ git commit -m "add initial files"
/* cp is the bash command of copy
/* -R means recursively copy
/* followed by the folder path to be copied
/* . means copy to the current folder
```

- push the local commits to remote repo
```sh
$ git push origin master
/* origin is the name of remote
/* master is the branch
```

- public back to GitHub
```sh
$  git config --global push.default simple
/* config the git push command to simple version
```
### git fetch and pull
Curent status of the local and remote repos: clean working directory and up-to-date with remote repo

- make a change of a local
```sh
$ notepad README.md /* change readme file so the local repo is not up to date with remote
$ git commit -am "update readme"
$ git status /* the local branch is one commit ahead of the remote branch
```

- if try to git push, it reads an error
- git pull: two commands in one: fetech + merge
```sh
$ git fetch /* update all local info based on remote repo
$ git pull 
/* merge everything from github
$ git push
```

Doing a pull or a fetech prior to any pushes is best practice

- update Repository and References
IF the remote repo is rename, then the local reference to the remote repo need to be updated
```sh
$ git remote -v
$ git remote set-url origin newURL /* update the remote repo URL to new URL
$ git remote -v /* now the local repo should point to the new URL
$ git remote show origin
```

### looking at, create, and edit files at GitHub
- If file is changed directly on Github, need to commit change on github
- When commit the change on github, a new branch can be created. 
- The action will triger a pull request to the master branch.
- So there will be a pull commit message editor and comment along with it
- Then click the create pull request
- The Merge pull request will be available. The pull commit message can be edited here. Then click confirm merge
- once the newBranch is merged with the master branch, the new branch can be deleted.


- Renaming and deleting files on Github

### Synchronizing Github changes on local repo
- There are severl commits made on the Github remote repo
```sh
$ git status /* local repo should be non-staging/all committed
$ git fetech /* update local references from remote github
$ git status /* message read that the local repo is behind remote repo by serveral commits
$ git pull /* This will update the remote commits to local repo
```

- Review commits with commits list
- Using CommitID with local git repo
```sh
$ git status
$ git pull
$ git show commitID /* CommitID can be found from the Github -> Commits
```

### Create Branches on Github
### Create local branch and push to github
```sh
$ git checkout -b newBranch /* create and switched to newBranch
$ git rm myfile.txt /* remove myfile.txt under newBranch
$ git commit -m "remove myfile"
$ git status /* back to clean working directory
```
All the changes are made locally. Back to remote github, there is no newBranch.

```sh
$ git push -u origin newBranch 
/* -u create tracking relationship
/* origin is the name of the remote
/* newBranch is created on Github
/* after that a tracking relationship is set up, means the two branches are sync with each other
/* If git pull or git push without specifying, this is the branch that it will be going to
```


### Comparing and Pull Requests
[reference](https://guides.github.com/activities/hello-world/#:~:text=Pull%20Requests%20are%20the%20heart,the%20content%20from%20both%20branches.)

When  you have changes in a branch off of main(master), you can open a pull request. 

Pull Requests are the heart of collaboration on GitHub. When you open a pull request, you’re proposing your changes and requesting that someone review and pull in your contribution and merge them into their branch. Pull requests show diffs, or differences, of the content from both branches. The changes, additions, and subtractions are shown in green and red.


As soon as you make a commit, you can open a pull request and start a discussion, even before the code is finished.

Open a Pull Request for changes to the README
1. Click the  Pull Request tab, then from the Pull Request page, click the green New pull request button.
2. In the Example Comparisons box, select the branch you made, readme-edits, to compare with main (the original).
3. Look over your changes in the diffs on the Compare page, make sure they’re what you want to submit.
4. When you’re satisfied that these are the changes you want to submit, click the big green Create Pull Request button.
5. Give your pull request a title and write a brief description of your changes.
6. When you’re done with your message, click Create pull request!
