---
layout: page
title: "Git"
permalink: /git/
---

#How to GitHub

*[Branching](#branching)

## Local git
Things that are done locally in a single branch, not changing anything in the remote repository.

### Set up

Set up name and email

	git config --global user.name <NAME>
	git config --global user.email <EMAIL>

Put directory under git revision control:
	
	git init

Check config information 

	git config -l

Set url in the `.git/config` file
	
	git remote set-url origin <address>.git

Push local branch to remote (master is the local branch name)
	
	git push -u origin master


### Basic commands

Steps of staging: 
Local repository -- <i>add</i> --> staged -- <i>commit </i>--> remote repository.

#### Viewing status
- Check git status.

		git status

- Check changes of files from two branches:
		
		git diff mybranch..master -- myfile.cs

- View commit history:
		
		git log

- Look at the new commit after clone:
	
		git log origin


#### Apply new changes
1. Add file to be commit:

    git add <FILENAME>

    Re-do it (unstage a file)
    	

    	git reset HEAD <FILENAME>

2. Commit file and push it to remote repository:

		git commit -m "Say something"

	remove commit and bring the file back as staged:
		
	
		git reset --soft HEAD~1		

#### Edit repository
- change added (to be commit) file:
		
		git mv <OLD-FILENAME> <NEW-FILENAME>		
		
	
	git rm <FILENAME>		
	
- retrieve commited file (to replace an unstaged file):
		
		git checkout --<FILENAME>		

#### Local Git management

- Copy a folder (with added/submitted files):

		git clone exited_folder new_folder

- Save log (a diff is called a patch):
	
		git format-patch --stdout origin > mywork.mbox


## Remote GitHub

- Clone: to copy a complete repository

		git clone https://github.com/Ooohu/Cross-section-calculator.git

- Pull: fetch + merg
		
		git pull <REMOTENAME> <BRANCHNAME>

- Fetch: to retrieve a file

		git fetch <REMOTENAME>

- Merge: combine remote-tracking branch with local branch:
		
		git merge <REMOTENAME>/<BRANCHNAME>


### Branching

#### Branching steps:
[Reference](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)

1. Create a new branch for a new particular issue; do this at your master branch.
2. Push the new branch (to overwrite the original branch), or based on the original branch, based on the new branch.

#### Single Branching
Look at current branches:

    git branch

Create a new branch and switch to it:

    $ git checkout -b <new_branch_name>
    
    which is equivalent the following
    
    $ git branch <new_branch_name>
    $ git checkout <(that)new_branch_name>

Clone a specific branch of git
	
	git clone --single-branch --branch feature/miniboone_Nov20 https://github.com/Ooohu/hellstroms_hive.git

Create a new branch

    git branch <branch_name>


Switch to a branch

    git checkout <branch_name>

Merge branch (bring the other branch into current branch)

    git merge <the other branch>

Merge branch from another repository

	git remote add <nickname_for_the_repository> <repository.git> #connect the repository
	git fetch <nickname_for_the_repository> #get the branches
	git merge <nickname_for_the_repository>/branch

Delete branch

    git branch -d <branch_name>

Rename a local branch
	
	git branch -m <oldname> <newname>
	# or rename the current branch:
	git branch -m <newname>

Check tag
	
	git tag


#### Cross Branching

Push a feature branch to target branch (will overwrite others' work):

    $ git push -u <target branch> <feature branch>

Check the difference beteen branches:

    $ git diff <branch1>..<branch2>

Checkout specific file from other branches:

    git fetch
    git checkout -m master <file name>

Merge a file from other branch:

    git checkout -p origin/master -- bdt_file.h   

`-p` mode lets you choose one path out of a status like selection. After choosing the path, it presents the diff between the index and the working tree file and asks you if you want to stage the change of each hunk. You can select one of the following options and type return:

      y - stage this hunk
      n - do not stage this hunk
      q - quit; do not stage this hunk nor any of the remaining ones
      a - stage this hunk and all later hunks in the file
      d - do not stage this hunk nor any of the later hunks in the file
      g - select a hunk to go to
      / - search for a hunk matching the given regex
      j - leave this hunk undecided, see next undecided hunk
      J - leave this hunk undecided, see next hunk
      k - leave this hunk undecided, see previous undecided hunk
      K - leave this hunk undecided, see previous hunk
      s - split the current hunk into smaller hunks
      e - manually edit the current hunk
      ? - print help


## Trouble Shooting

### Username

Error looks like:
	
	error: The requested URL returned error: 403 Forbidden while accessing 


>Change your `url` in `.git/config`, chenge the address to the format:
> `<username>@github.com/<repository>`
> or
> `git@github.com:Ooohu/<repository>`
> 
> Or try this
> 	`git config --get-all <name>`



```Permission denied (publickey).
Permission denied (publickey).
fatal: The remote end hung up unexpectedly
```

> [ref](https://stackoverflow.com/questions/19660744/git-push-permission-denied-public-key) 
> Generate ssh key and copy it to github account (in the setting session)
>
> ```
> cd ~/.ssh
> ssh-keygen
> ```
>
> The key will be found in:
>
> ```
> ~/.ssh/id_rsa.pub
> ```
>
> Then build the ssh connection
>
> ```
> ssh -T git@github.com
> ```

