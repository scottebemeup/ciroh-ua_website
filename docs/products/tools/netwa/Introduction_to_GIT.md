# Agenda

[The Case for Code Versioning](#getting-a-repository)

[Getting a Repository](#getting-a-repository)

[Configuring GIT](#configuring-git)

[Making and Saving Changes](#making-and-saving-changes)

[Ignoring Files](#ignoring-files)

[Sharing Changes](#sharing-changes)

[Content History](#content-history)

[Branch Management](#branch-management)

[Resolving Merge Conflicts](#resolving-conflicts)

[Undoing That Thing You Just Did](#undoing-your-work)


## The Case for Code Versioning
============================
* Versioning maintains snapshots of edited code, over time, with the ability to move forward and backward along that timeline
  * Save your brilliant idea for the whole team to use
  * Undo that unfortunate choice that ignored a fundamental assumption
* The timeline may include forks and mergers of experiments tried and abandoned or propagated
  * Try three things, test them in parallel, and keep the one you like best
  * Change your mind and pick the other option that was almost as fast, but is more flexible
* A single developer may benefit from code versioning, but a team of developers jointly modifying pieces of one project is likely to not succeed without code versioning
  * That elegant algorithm your teammate wrote can't be used until you share your updated data prep step
  * The person testing the code you shared last week needs a quick fix, but you are half way through a new, major update

## GIT for Code Versioning
=======================
* GIT is a Utility/App/Program to facilitate managing code versions
* First created in 2005 as part of Linux Development Environment
* Support Multiple Local Repositories that can be Conditionally Synchronized with each other
* Each Developer can have their own copy of everything, and can share updates with all, or some of, the other developers as they are ready for use

## Basic Git Commands
------------------
* git **clone** : to create a local repository connected to a remote copy
  * Often points to a central copy referenced as the "Origin"
  * **git clone git@gitlab.uvm.edu:vermont-epscor/cyberinfrastructure.git cyberinf**
* git **status** : to assess the state of a local repository
  * List any untracked files or tracked files with uncommitted changes
* git **add** : to add a new or updated file to the list of updates to be tracked
   * Adds a file to the list to be included in the next commit
* git **commit** : to formally commit a set of updates to a new snapshot of content
  * Bundle all pending added changes into a retrievable snapshot
* git **push** : share an updated local repository to update the central copy
* git **pull** : update a local repository with updates from the central copy

## Getting a Repository
* git clone
  * used to create a local copy of a remote repository
  * registers the remote repository as the origin of the copy
  * need to know the URL where the remote content is served from (i.e. our gitlab area)
  * `git clone git@gitlab.uvm.edu:vermont-epscor/cyberinfrastructure.git name`

* git pull
  * used to obtain the updates present at the remote origin
  * will merge new content into your current local working copy
  * `git pull`
  * `git pull origin master`

* git fetch
  * used to get content from a remote repository
  * does not merge content into your local working copy

## Configuring GIT
* $HOME/.gitconfig
  * a user specific file to make settings common across repositories
  * editor selection
  * merge tool specification
  * diff tool specification
* `git config --list`   to list all your configuration settings

> #### List of config contents from a Linux Install
> ```
> [seturnbu@epscor gitdemo]$ git config --list
> user.name=Scott Turnbull
> user.email=seturnbu@uvm.edu
> diff.tool=meld
> merge.tool=meld
> difftool.meld.cmd=meld "$LOCAL" "$REMOTE"
> mergetool.meld.cmd=meld "$LOCAL" "$BASE" "$REMOTE" --output "$MERGED"
> core.repositoryformatversion=0
> core.filemode=true
> core.bare=false
> core.logallrefupdates=true
> remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
> remote.origin.url=git@gitlab.uvm.edu:vermont-epscor/cyberinfrastructure.git
> branch.master.remote=origin
> branch.master.merge=refs/heads/master
> ```


* Updating the config
  * edit the files in a wise and knowing manner
  * use commands to set specific configuration options
      * `git config --global user.name "John Doe"`  to set your user name
      * `git config --global user.email johndoe@uvm.edu`  
      * `git config --global core.editor emacs`   to set the default editor to emacs
      * `git config --global diff.tool meld`  to set the default diff tool to meld
      * `git config --global difftool.meld.cmd 'meld "$LOCAL" "$REMOTE"'`



> #### Contents of a Windows OS .gitconfig has different path syntax
>```
>$ cat $HOME/.gitconfig
>[user]
>	email = seturnbu@uvm.edu
>	name = Scott Turnbull
>[gui]
>[push]
>	default = simple
>[gui]
>	recentrepo = C:/Users/scott.turnbull/Documents/EPSCoR/git/newrnetabm
>	recentrepo = C:/Users/scott.turnbull/Documents/EPSCoR/git/lutabm
>[diff]
>	tool = meld
>[difftool "meld"]
>	cmd = \"C:/Program Files (x86)/Meld/Meld.exe\" \"$LOCAL\" \"$REMOTE\"
>[merge]
>	tool = meld
>[mergetool "meld"]
>	cmd = \"C:/Program Files (x86)/Meld/Meld.exe\" --auto-merge \"$LOCAL\" \"$BASE\" \"$REMOTE\" ---output \"$MERGED\" --label \"MERGE (REMOTE BASE MY)\"
>```


* repository/.git/config
  * repository specific configuration
    * specification of the remote repository
    * branch names
  * is dynamically updated by GIT as you work with your repository
  * can be used to create a repository specific setting that differs from global file

> #### Contents of Repository Specific .git/config
>```
> $ cat config
> [core]
>         repositoryformatversion = 0
>         filemode = false
>         bare = false
>         logallrefupdates = true
>         symlinks = false
>         ignorecase = true
> [remote "origin"]
>         url = git@gitlab.uvm.edu:vermont-epscor/cyberinfrastructure.git
>         fetch = +refs/heads/*:refs/remotes/origin/*
> [branch "master"]
>         remote = origin
>         merge = refs/heads/master
>```



## Making and Saving Changes

* They're "just" files. Change content as you always have

![alt text]( 
https://git-scm.com/book/en/v2/images/areas.png
"Local Directory WorkFlow")


* `git status`  to list the files that have local changes
  * lists changes to be committed (staged)
  * lists changes not staged for commit
  * identifies new files (staged or unstaged)
  * lists tracked files that have been deleted

> #### Status of repository with staged new file and unstaged modification
> ```
> $ git status
> On branch master
> Your branch is up-to-date with 'origin/master'.
> Changes to be committed:
>   (use "git reset HEAD <file>..." to unstage)
> 
>     new file:   README
> 
> Changes not staged for commit:
>   (use "git add <file>..." to update what will be committed)
>   (use "git checkout -- <file>..." to discard changes in working directory)
> 
>     modified:   CONTRIBUTING.md
> ```


![alt text](https://git-scm.com/book/en/v2/images/lifecycle.png "File Workflow")

* git add - the simple use
  * `git add myfile.txt` to stage a single file
  * `git add myfile1.txt myfile2.txt` to stage a list of files
  * `git add myfile*.txt` to stage files using wildcarding
  * `git add .`  stages new and modified in the current directory and below, without deleted
  * `git add -u` stages modified and deleted, without new
  * `git add --all` to stage everything in all dirs that isn't already tracked or staged (CAUTION!)

* git add - much more subtlety and power lurks under many options 
    * `git add [--verbose | -v] [--dry-run | -n] [--force | -f] [--interactive | -i] [--patch | -p]
	  [--edit | -e] [--[no-]all | --[no-]ignore-removal | [--update | -u]]
	  [--intent-to-add | -N] [--refresh] [--ignore-errors] [--ignore-missing]
	  [--chmod=(+|-)x] [--] [<pathspec>…​]`
    * Note that file content is staged at the time of the `git add`
    * A file modified, staged, then re-modified, shows as staged and not staged

> #### Status with a staged modified file that has a 2nd modification
> ```
> $ git status
> On branch master
> Your branch is up-to-date with 'origin/master'.
> Changes to be committed:
>   (use "git reset HEAD <file>..." to unstage)
> 
>     new file:   README
>     modified:   CONTRIBUTING.md
> 
> Changes not staged for commit:
>   (use "git add <file>..." to update what will be committed)
>   (use "git checkout -- <file>..." to discard changes in working directory)
> 
>     modified:   CONTRIBUTING.md
> ```

* `git rm`  to stage the removal of any files for the next commit

* git commit
  * `git commit -m "meaningful message"`   commits all staged content to the local repository
  * `git commit -a -m "helpful description"`  automatically does an add for modified tracked files
  * `git commit --amend`   add staged information to the previous commit

## Ignoring Files
* sometimes there are files in a repository directory that we may not want git to process
  * files derived from source (*.o, *.pyc, *.jar)
  * files autosaved from editors (*.bak)
  * data files
  * output files
* .gitignore
  * specify name patterns of files that git should ignore
      * *.pyc
      * *.[oa]
      * *.bak
  * specify directory names to exclude
      * datadir


## Sharing Changes
* git push 
  * `git push origin master`
  * `git push --dry-run`   will prepare the push, generate any messages, but make no changes
* git pull

## Content History
* git log
* git tag
  * `git tag`   list of all defined tags
  * `git tag -l "partial*"`  list tags matching a wildcarded name
  * `git tag -a thetag -m "Good description"`  create a new annotated tag
  * `git tag -a goodtagname 9fceb02`   to tag a previous commit identifier
  * `git push origin --tags`   pushes all tags to the origin, alternatively they can be named
* git diff
* git show
  * `git show thetag`   list information about a tag
* git checkout
  * `git checkout thebranch`  to switch context to a branch
  * `git checkout thetag`   to switch context to a tagged commit (beware the HEADless context!)


## Branch Management
* git branch
  * `git branch`   list the current branches
  * `git branch testing` create a branch
* git checkout
  * `git checkout master`  selects master branch
  * `git checkout testing` selects testing branch
  * `git checkout -b newbranch` create and checkout a new branch
  * currently selected branch pointed to by **HEAD**

![alt text](https://git-scm.com/book/en/v2/images/advance-testing.png "Straight Branch Example")

![alt text](https://git-scm.com/book/en/v2/images/advance-master.png "Split Branch Example")

## Resolving Conflicts
*  `git diff`
  * displays differences between two copies of content
*  `git merge`
  * attempts to reconcile differing content copies into a merged result
  * invoked under the covers of a `git pull`
* `git merge <branch_name>` merge updates made to "branch_name" to the current branch
* `git mergetool`  launches a graphical merge tool to guide the resolution of conflicts

## Undoing Your Work
* `git stash`  moves local edits to a side directory to avoid a merge conflict
* `git checkout` undoes unstaged edits
* git reset HEAD 
  * unstages a file
* git revert
  * undoes a commit
* `git merge --abort` undoes a merge conflict by by unspooling commits it made

## Resources

GIT Documentation - https://git-scm.com/docs
* https://git-scm.com/book/en/v2/Getting-Started-Git-Basics
* https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository

https://dev.to/exwhyzed/how-to-git-a-complete-beginners-guide-1h85
https://dev.to/lydiahallie/cs-visualized-useful-git-commands-37p1  
https://dev.to/milu_franz/git-explained-the-basics-igc

Software Carpentry Version Control Lecture and Labs
https://swcarpentry.github.io/git-novice/

* Introduction to Version control
  * https://swcarpentry.github.io/git-novice/01-basics/
* Setting up GIT
  * https://swcarpentry.github.io/git-novice/02-setup/
* Collaboration using GIT
  * https://swcarpentry.github.io/git-novice/08-collab/
* Ignoring Files
  * https://swcarpentry.github.io/git-novice/06-ignore/
* Resolving Conflicts
  * https://swcarpentry.github.io/git-novice/09-conflict/
* History
  * https://swcarpentry.github.io/git-novice/05-history/

