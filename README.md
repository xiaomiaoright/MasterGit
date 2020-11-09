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

### Merging Locally (Merge branch)
Integrate changes in other branches into the master branch.

```sh
$ git status
$ git checkout master /* switch back to master
$ git pull /* keep the master branch up to date with the remote
$ git merge newBranch
/* prompt for merge message
$ git push /* synchronize local changes back to github
```

- Remove a branch locally
```sh
$ git branch -a /* list all the branches
$ git branch -d newBranch /* remove new branch
$ git branch -a
```
The local newBranch is deleted but there is still the reference to remote branch reference.

```sh
$ git fetech -p /* prune option. look for dead branches and remove these references
```

- Locally switch to a branch in github
- Create a branch on github
```sh
$ git status
$ git branch -a
/* since a newBranch is created on remote Github, so fetech the changes locally
$ git fetch
$ git branch -a
$ git checkout newBranch /* now the local newBranch and remote newBranch are tracked
```
- make some update in the local newBranch
```sh
$ notepad README.md
$ git commit -am "update readme"
$ git push /* git will push the changes to the tracked newBranch on github
```

- Clean up by deleting branches and references
```sh
$ git checkout master /* switch back to master
$ git pull /* without specifying branches, git will pull from master branch on Github
$ git pull --all /* git hub update all tracking branch
$ git merge
$ git push /* push local master to remote master
$ git branch -d newBranch /* delete local branch, but remote newBranch is still there
```

- Delete a remote branch from a command line
```sh
/* currently under the local master branch
$ git push origin :newBranch
/* using git push with args
/* origin is the name of the remote
/* followed by a ":", telling git anything followed the ":" should be deleted
/* newBranch is the remote Branch to be deleted
$ git branch -a
```

### pull with rebase
- rebase: rewinds the current commits on your branch to a point where the branch you are merging in originally diverged
- rebase can make sure whatever changes made on local is ahead of remote

1. local and remote repo are up to date
```sh
$ git status
$ git pull /* make sure everything is up to date
```
2. make some changes on remote github and commit. Remote git repo is one commit ahead of local
3. make some changes on local git repo and commit. Now both local and remote git repo have one commit out of date
4. If run git fetech, git will update the local repo with whatever updates make on remote
```sh
$ git fetch
```
5. run git status. Git shows local and remote have diverged. 1 and 1 commit different from each other. 
```sh
$ git status
```
6. Git merge is an option. But to make sure the local repo is ahead of the remote, use  rebase first
```sh
$ git pull --rebase
```
/* rebase means git will pull the remote commits first before the local commits.
7. run git hist to check the pulled remote commits and local commits
```sh
$ git hist
```
8. push changes to github
```sh
$ git push
```
- Github Graphs and Networking
```sh
$ git log --oneline --graph /* press q to quit
```

- change default branch on github

    In production, master branch should not be the active development branch. Instead, there should be  long live development branch, where changes can be made. When the product is ready to release, merge the development branch to master branch.

    - Change the default branch on github repo setting
    - when the default branch (develop) is changed, when create a pull request, the base branch will be the default branch
    - When clone the github repo to local
        - local repo has develop branch, but does not have a master branch
        - develop branch is set up as tracking branch at local
        - if want to get the master branch on local, will need to checkout the develop branch and fetch it down from the remote repository
        ```sh
        $ git checkout master
        /* since there is no master branch local, git goes to remote and brings in origin/master branch, and set that up as local master branch
        $ git branch -a
        /* check all the branches local, it should show both master and develop
        ```
- Deal with conflicts when pulling
```sh
/* first make sure local and remote are up to date
/* create a problemetic change on remote repo and commit
$ git fetch /* copy everything from repo to local
$ git status /* now can see that origin/develop branch is one commit ahead

/* make local changes on the same file on local repo and commit
$ git commit -am "Update readme local"
$ git status /* now it shows local develop branch and remote origin/develop branch diverged
$ git pull /* fetch + merge, it will bring in merge error and enters the develop|MERGE status
$ git mergetool /* use the configed git merge tool to resolve the conflicts
$ git commit -m "resolving the merge conflict with merging tool" /* commit the conflict resolving and the repo should exit the develop|MERGE status
$ git status /* so local repo is ahead of remote 2 commits and README.md.orig file is not staged which should be removed
$ rm *.orig /* remove the original README.md.orig file
$ git push /* push develop to remote develop
/* go to github and reload, should see the changes
```

### Github Tags and Releases
- create local tags (simple and lightweight tags)
```sh
$ git status /* check the current working directory is clean
$ git log --oneline /* check the commits history
/* create several tags to mark major milestones in this repo based on the commit list
$ git tag /* check the current available tags

/* create simple and lightweight tags, no extra info
/* create a tag unstable to reference the HEAD position (last commit of the current branch)
$ git tag unstable develop /* create tag unstable to reference to the last commit of develop branch
$ git tag stable master /* create tag stable to reference to the last commit of master branch
$ git hist
```

- create release tags or annotated tags
```sh
$ git tag -a v0.1-alpha -m "Realse 0.1 (Alpha)" 85fe102 /* -a mean annotated tag and 85fe102 is the commit
$ git tag /* should show 3 tags now
/* for annotated tags can use git show 
$ git show v0.1-alpha /* show tag info and related commit info
/* in this way can create more annotated tag
```

- push local tags to remote github
```sh
$ git pull /* make sure everything up to date
/* by default, git push will not push the tags
/* need to use git push command specifying the tags to push
$ git push origin stable /* origin is remote name, stable is the tag name
$ git push --tags /* push all the tag
```

- tags in Github

For lightweighted tags, it will only show commit message
For annotated tags, it will show the corresponding tag message

- Deleting tags on Github
```sh
/* delete a tag on Github
/* but the tag still in local
$ git fetch -p /* fetch all the current reference 
/* delete the tag on local
$ git tag -d v0.1-alpha
```

- delete tags local first
```sh
$ git tag -d v0.2-alpha
$ git push origin :v0.2-alpha /* it will show the remote tag is deleted
```

- Updating tags Floating tags
```sh
$ git status
/* make some changes
$ git commit -am "update change"
$ git push 
$ git log --oneline --decorate
/* update an existing tag to the latest commit
S git tag -f unstable 426900a 
/* -f means update tag
/* unstable is tag name
/* 426900a is the commit to reference to. if blank, point to the last commit
$ git log --oneline --decorate
$ git pull
$ git push /* push the changes to remote, but the tags is not pushed
$ git push --force origin unstable 
/* stable already exits in remote, git push will result in conflict
/* --force will force the new tag to github
```

### Starting a release on Github
- GitHub realease is together with tags
- Under the Tags tab, there is option of Add release nots
- Click Add release notes, will lead back to the release to write release notes
- Push release

- Delete a Release

- create a completely new release
    - Releaes > new release
    - It will create a related tag the same time
```sh
$ git checkout master /* new created release on github is on master
$ git tag
$ git pull
$ git show V1.0 /* if V1.0 no info, it means it is light tag
```


### Compare on GitHub with Pull Requests
- compare commits
- compare tags

## Social Coding
Fork a public repository, contribute, and send it back by creating pull request. By Fork a public repo on Githuh, it will create a copy of the repo to your account. Then you can work on the code on the repo of your own account.
1. create a branch first
2. clone the repo to your local and make changes
3. create a pull request

```sh
$ git clone localRepoURL
$ cd localRepo /* change the path to local repo folder 
$ git checkout -b feature-readme /* create a new branch to save our work
$ notepad README.md /* create a readme file
$ git commit -am "update readme file"
$ git push -u origin feature-readme /* push the changes to repo
```

1. Go to github repo and check the new created branch
2. Click Compare and pull request or within in the branch, click the pull request button
3. by default, the pull request will set up relationship back to the upstream repository (not my github repo, but where the repo forked from)
4. Once confirmed the relationship, click create a Create Pull Request
5. It will load to the target/parent repo once the request is created

- Update pull request
1. go the parent repo and check Pull request 
2. Go the your pull request
3. Available options:
    - Edit title of the pull request
    - Assign labels, milestones, assignees for review
    - Add more commits to the feature-readme branch 
4. Available tabs:
    - Conversation
        - conversation
        - Whether it can be merged with based branches
    - Commits
    - Files changed
```sh
/* update readme file again
$ git commit -am "update the readme again"
$ git status /* one commit ahead
$ git push /* push the commit back to my github repo
```
Now check the parent repo (where forked from), the pull request is updated with the last commit as well.

- Review and accept pull request

As the user of the public repo (where forked from), go to pull request. Go to the pull request you are interested in reviewing. Available options: Conversation, commits, FilesChanged; Merge pull request

    - Add comment  with markdown
    - Merge pull request
        - add merge message
    - revert the pull request

Go back to my personal github repo (where forked to) and check the Pull Request, it will show a merge icon under title

    - Under the pull request, Delete branch is available

- Github graphs
- Synchronize changes back to your work
```sh
/* go the parental repo (where forked from) and copy repoURL
/* git bash prompt and cd to the local repo folder and checkout your branch
$ git status /* clean
$ git remote -V /* Verbose, show all remote repository references
/* Other remote references can be added
$ git remote add upstream repoURL /* upstream is the name of the new reference
$ git remote -V /* the list should include the newly create upstream reference
$ git pull upstream master /* pull from upstream to local master branch
$ git push origin master /* push changes to my remote repo (where forked to)
```

Clean up the working directory

```sh
$ git branch -a
$ git branch -d feature-readme
/* if didnt integrate the changes from the upstream repo, feature-readme branch wont be updated on my github repo. Git will show error if delete it
$ git branch -a /* it should only one master branch now. But there are reference to the remote branches. However, check the remote github branch, there is only one master branch only. So fetech the remote repo to local to remove these references.
$ git fetch -p /* -p mean prune option
/* git will go to the github remote repo and notice branches deleted. So it will delete the reference to that branch
```

## FAQ

1. How to activate conda environment in Bash?

```sh
$ eval "$(conda shell.bash hook)"
$ conda activate <env-name>
```
