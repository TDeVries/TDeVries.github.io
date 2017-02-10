---
layout: post
title: How to Use Git and GitHub
description: "Summary of Udacity's 'How to Use Git and GitHub' course."
modified: 2017-01-25
tags: [Git, Github, Udacity]
---

I recently worked my way through Udacity's [_How to Use Git and GitHub_](https://www.udacity.com/course/how-to-use-git-and-github--ud775) course, which I would highly recommend to anyone who wants to learn how to use Git but has no idea where to start. Git is a version control system (VCS) that can be used to track changes made to files on a computer. This capability makes it extremely useful for tasks like computer programming, where files are constantly being modified and updated with new features, bug fixes, or documention. Github enhances upon Git by making files available online for you or other collaborators.

_How to Use Git and GitHub_ provided a great overview on how Git and Github operate under the hood, introduced all of the Git commands that one would need in order to use Git proficiently, and most importantly, the course provides examples and quizzes so that you can get familiar with each of the new concepts as soon as they are introduced. What follows is a summary of the content from the course, but if you have the time the full course is certainly worth it! 


## Git Installation
Udacity provides instructions on how to install Git for different operating systems, which you can find [here](https://www.udacity.com/wiki/ud775/install-git).


## Setting Up Your Git Workspace
To set up your Git workspace first save git-completion.bash and git-prompt.sh to your local home directory:

[git-completion.bash](https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash) - Enables tab completion for Git commands.  
[git-prompt.sh](https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh) - Enables Git features in the terminal prompt, such as displaying the commit ID or branch name of your current location within the repository.

Next create a file called .bash_profile in your home directory (or .bashrc for Linux) and copy the following lines into it, or copy them to the bottom of the file if it exists already. 

```bash
# Enable tab completion
source ~/git-completion.bash

# colours!
red="\[\033[0;31m\]"
green="\[\033[0;32m\]"
yellow="\[\033[0;33m\]"
blue="\[\033[0;34m\]"
magenta="\[\033[0;35m\]"
cyan="\[\033[0;36m\]"
default="\[\033[0;39m\]"
reset="\[\033[0m\]"

# Change command prompt
source ~/git-prompt.sh
export GIT_PS1_SHOWDIRTYSTATE=1
# '\u' adds the name of the current user to the prompt
# '\$(__git_ps1)' adds git-related stuff
# '\W' adds the name of the current directory
# You can change the colours in the command below to customize
# 	the terminal prompt to your liking. Available colours
# 	are listed above.
export PS1="$green\u$red\$(__git_ps1)$default \W $ $reset"
```

Once finished restart your terminal (or Git Bash) to enable the changes.

### Useful Git Config Commands

The following are some useful commands which can be used to configure your Git settings. Simply enter them into your terminal (or Git Bash).

`git config --list`: Displays your current configuration settings.  

`git config --global core.editor "'C:/Program Files/Sublime Text 3/sublime_text.exe' -n -w"`: Sets the text editor that you will use to enter notes for the commit log. If not using Sublime then substitute in the file path to your favourite text editor. The editor must be capable of being launched from command-line.  

`git config --global push.default upstream`: Sets the default action for `git push` so that it will push the current branch to its upstream branch.  

`git config --global merge.conflictstyle diff3`: When a merge conflict is encountered Git will show, side-by-side, your version of the code, the code snippet that it is conflicted with, and the common ancestor between them. 

`git config --global color.ui auto`: Enables coloured diff output.  

`git config --global core.autocrlf true`: Prevents merge conflicts that may occur when working with files from Unix or Mac systems (they use a different newline character scheme).  

`git config --system core.longpaths true`: Allows Windows to work with file path names that are longer than its limit [Windows only].  


## Git Usage Tips
* The master branch should be reserved for your production quality code. It should always be in working condition.
* A development branch can be created as a place for active work on the code base. It is common to make a new branch for each new feature of bug fix. Once a feature from the development branch is working it becomes the new master branch, or can be merged with the master branch.
* An experimental branch could also be created for unique features or stuff that you expect to break the code.


## Git Commands

#### For displaying information  
`git log`: Displays all of the commits previously made.  

`git log --graph --oneline [branch_name_1] [branch_name_2]`: Shows branch structure of repo, with each commit as one line to save space.

`git diff [commit_ID_1] [commit_ID_2]`: Shows the difference between two commits, displaying only the lines that have changed. It is assumed that commit_ID_1 is the original and commit_ID_2 is the modified version.  

`git diff`: Compares files in staging area with those in working directory. Shows changes that haven't been staged yet.  

`git diff --staged`: Shows difference between files currently in staging area and files in the repository.

`git show [commit_ID]`: Shows a diff of a commit and it's parent (the commit that this one modified). Useful if you have merged branches and commits are mixed due to timestamp ordering.

#### Regarding commits
`git init`: Creates a new repository in your current directory. All subdirectories are automatically included in the repository.  

`git add [file_name]`: Adds the specified file to the staging area.  

`git status`:  Shows you all of the files that are currently in the staging srea, and all of the files that have not yet been committed. 

`git reset [file_name]`: Removes a file from the staging area.  

`git reset --hard`: Warning - Discards any changes in staging area or working directory. Not reversible.  

`git commit`: Commits files in staging area into repository.  

`git commit --amend`: Edit the commit message for the commit that is currently checked out.

`git commit -m ["Commit message in quotes"]`: Commits using the provided commit message instead of opening a text editor.

`git checkout [commit_ID/branch_name]`: Reverts all files in repository to the state they were at when the specified commit was made.

#### Regarding branches

`git branch`: Displays all of the existing branches.  

`git branch [new_branch_name]`: Creates a new branch with the specified name, copied from the current branch.  

`git checkout -b [new_branch_name]`: Equivalent to creating a new branch and then checking it out.  

`git branch -d [branch_name]`: Caution - Deletes a branches label. Branch may be difficult or impossible to access anymore.

`git merge [branch_name_1] [branch_name_2] ... [branch_name_n]`: Merge multiple branches into a single commit, *_including the current branch_*)  

`git merge --abort`: Run this command if you get conflict errors when attempting to merge and want to cancel the process.

#### Interfacing with Github
Note 1: You will need to set up a repository on Github first before you will be able to push commits to it.   
Note 2: When you clone a repository on Github it will automatically set up a remote for you to pull/push to.   

`git clone [URL/filepath]`: Make a copy of a repository from the specified URL or filepath. Copies all existing commit history.

`git remote`: Show existing remote repositories.  

`git remote -v`: Verbose output, use to check the remote repository's URL.  

`git remote add [remote_name] [remote_URL]`: Link the local repository with a remote repository. remote_name is usually set to 'origin', URL is the path of the Github repo we want to save stuff to.

`git push [remote_name] [branch_name]`: Push local repo to Github. Need to define which remote to send it to, and which branch to send.  

`git fetch [remote_name]`: Creates a new local branch for any changes in the Github repo that are different from your local repo.  

`git pull [remote_name] [branch_name]`: Pull Github repo to local repository. Equivalent to git fetch + git merge.

## Useful Links
[Udacity git commit style guide](https://udacity.github.io/git-styleguide/)  
[Git cheat sheet](https://github.com/github/training-kit/blob/master/downloads/github-git-cheat-sheet.pdf)  
[How to cache your Github password](https://help.github.com/articles/caching-your-github-password-in-git/#platform-windows)
