



# Table of Content:

1.  [Senarios](#Senarios)
2.  [Often used Git commands](#Often-used-Git-commands)
   1.  [Clone into differently named folder](#Clone-into-differently-named-folder)
   2.  [To highlight words instead of lines with diff](#To-highlight-words-instead-of-lines-with-diff)
   3.  [Compare a file between 2 commits](#Compare-a-file-between-2-commits)
   4.  [To create a new branch](#To-create-a-new-branch)
   5.  [To delete a remote branch](#To-delete-a-remote-branch)
   6.  [To delete a local branch](#To-delete-a-local-branch)
   7.  [To go back one local commit with files still being ready for commit](#To-go-back-one-local-commit-with-files-still-being-ready-for-commit)
   8.  [When on feature branch rebase to sync it back up with master](#When-on-feature-branch-rebase-to-sync-it-back-up-with-master)
   9.  [Find when file was added](#Find-when-file-was-added)
   10. [Restore empty working tree](#Restore-empty-working-tree)
   11. [git cannot detect changes in file names between high and low case](#git-cannot-detect-changes-in-file-names-between-high-and-low-case)
   12. [When on master how to merge a branch into master](#When-on-master-how-to-merge-a-branch-into-master)
   13. [After pulling from a repo and it says “(new commits)”](#After-pulling-from-a-repo-and-it-says-“(new-commits)”)
   14. [To get the diff without having to scroll through it, use -P](#To-get-the-diff-without-having-to-scroll-through-it,-use--P)
   15. [Look at last commit](#Look-at-last-commit)
   16. [If you want to save output of a command](#If-you-want-to-save-output-of-a-command)
   17. [List all tags](#List-all-tags)
   18. [To temporarily hide your changes use](#To-temporarily-hide-your-changes-use)
3.  [Interact with git stash'es](#Interact-with-git-stash'es)
   1.  [show status, but only shows folders that are not tracked](#show-status,-but-only-shows-folders-that-are-not-tracked)
   2.  [Show status of files not yet tracked](#Show-status-of-files-not-yet-tracked)
   3.  [Get a list of all remote branches](#Get-a-list-of-all-remote-branches)
   4.  [Show the entire command reply instead of using the pager](#Show-the-entire-command-reply-instead-of-using-the-pager)
   5.  [To see what remote you are pointing to](#To-see-what-remote-you-are-pointing-to)
   6.  [To change what remote you are pointing to](#To-change-what-remote-you-are-pointing-to)
4.  [Git help syntax](#Git-help-syntax)
   1.  [git commands are written in kebab case](#git-commands-are-written-in-kebab-case)
   2.  [Angle brackets: <> means placeholder text](#Angle-brackets--means-placeholder-text)
   3.  [Dash: -<a-letter> means single letter short form of an argument](#Dash--a-letter-means-single-letter-short-form-of-an-argument)
   4.  [Double dash: --<word-or-words> is the long form of an argument](#Double-dash---word-or-words-is-the-long-form-of-an-argument)
   5.  [Pipe: <option-1> | <option-2> means use either](#Pipe-option-1--option-2-means-use-either)
   6.  [Square brackets: [] means an optional thing](#Square-brackets--means-an-optional-thing)
   7.  [double dashes alone: [--] means done with options](#double-dashes-alone----means-done-with-options)
5.  [Git term Definitions](#Git-term-Definitions)
   1.  [Repository](#Repository)
   2.  [Workspace/working tree](#Workspaceworking-tree)
   3.  [Index/Cache/Staging area](#IndexCacheStaging-area)
6.  [Merge conflicts tips](#Merge-conflicts-tips)
7.  [Basic workflow](#Basic-workflow)
   1.  [Create a development branch](#Create-a-development-branch)
   2.  [Develop your thing](#Develop-your-thing)
   3.  [Rebase your branch](#Rebase-your-branch)
      1.  [Make sure you have latest origin](#Make-sure-you-have-latest-origin)
      2.  [Rebase your branch](#Rebase-your-branch)
      3.  [Merge the branches](#Merge-the-branches)
   4.  [Short version](#Short-version)
8.  [git on windows](#git-on-windows)
   1.  [git working with paths longer than 260 characters on windows](#git-working-with-paths-longer-than-260-characters-on-windows)
9.  [github](#github)
   1.  [github on windows](#github-on-windows)










**When your code is breaking at 2am**
**Git will save you!**

/o/
 O
||
__Gitman!__



# Senarios:

1: What have I changed?
2: When did this happen?
3: Who did this?
4: Why is this like this?



# Often used Git commands

## Clone into differently named folder
git clone <git-repo.git> <fancy-new-folder>



## To highlight words instead of lines with diff
use
git diff --word-diff <The-file>



## Compare a file between 2 commits
git diff <commit-id-1> <commit-id-2> <file-you-want-to-compare>



## To create a new branch
git checkout -b my_fancy_branch_name



## To delete a remote branch
git push origin -d branch-name.



## To delete a local branch
git branch -d old-branch.



## To go back one local commit with files still being ready for commit
git reset --soft HEAD~1
If you then want the remote to also go back one commit then 
git push -f



## When on feature branch rebase to sync it back up with master
git pull origin master --rebase
git push -f
(If commits have been squashed then simply type “git rebase --continue” until you have skipped all your commits that are in fact in the squashed commit)


## Find when file was added
git log --diff-filter=A -- <your-file.txt>

## Restore empty working tree:
git commit -m'for now'
git checkout -f
git reset --soft HEAD~1



## git cannot detect changes in file names between high and low case
You poke git to detect it with
git mv <Source> <Destination> 



## When on master how to merge a branch into master
To ensure everything is 100% fine or the merge fails, we add the fast forward only argument
git merge --ff-only <your-development-branch-name>



## After pulling from a repo and it says “(new commits)”
That is because the sub-modules are not automatically pulled when the main one is. Fix this with the command:
git submodule update --init --recursive



## To get the diff without having to scroll through it, use -P
git -P diff <absolute path to file>



## Look at last commit
git log --name-status HEAD^..HEAD



## If you want to save output of a command
git blame file.name > output.txt

git log -p -- filename > output.txt



## List all tags
git tag -l *
Note that you can modify the wildcard to be more specific.



## To temporarily hide your changes use
git stash
git stash pop

# Interact with git stash'es
To see all saved stashes:
git stash list
To delete all saved stashes
git stash clear


## show status, but only shows folders that are not tracked
git status



## Show status of files not yet tracked 
git status -u



## Get a list of all remote branches
git branch -r



## Show the entire command reply instead of using the pager
git config --global core.pager "cat"
This is equivalent to starting a command with “git -P”



## To see what remote you are pointing to
git remote -v



## To change what remote you are pointing to
git remote set-url origin THE_NEW_ORIGIN





# Git help syntax

## git commands are written in kebab case
Meaning replacing spaces with dashes
so a command might look like this:
    git my-weird-command



## Angle brackets: <> means placeholder text
so
    git a-weird-command <path-to-file>

could be called like 
    git a-weird-command "/home/moose/Desktop/teaching_git/git notes.md"

notice I put the path in quotations because it have 2 spaces.
This is to avoid git thinkink it is 3 different argument



## Dash: -<a-letter> means single letter short form of an argument
For example, the short for for help in the git command is
git -h



## Double dash: --<word-or-words> is the long form of an argument
for example
git --help



## Pipe: <option-1> | <option-2> means use either
so a git command
    git weirdest-command --create-farbucket | --fill-bucket-with-fart

could be called like this:
    git weirdest-command --create-farbucket
or like this:
    git weirdest-command --fill-bucket-with-fart



## Square brackets: [] means an optional thing
so
    git weird [<path>] <author>
could be called
    git weird moose
or
    git weird "/home/moose/Desktop/teaching_git/git notes.md" moose

This can also show up in the argument explanations
so for example if you write
    git show -h
one of the lines looks like this:
    -q, --[no-]quiet      suppress diff output

meaning you can write
    git show --quiet
to run the command quiet
or
    git show --no-quiet
to run the command NOT quiet :3



## double dashes alone: [--] means done with options
This is to fix when it is not possible for git to distinguish when the options are done
and the following arguments start.
so if you have (for some reason) named a file "main" and you have a branch called "main"
now you want to revert changes to that file and call
    git checkout main
git... now defaults to switching to the branch main
so if you want to revert the changes you call it like this
    git checkout -- main
and it works! :D





# Git term Definitions

## Repository

This is technically the hidden folder called “.git”.

It is all the files GIT uses to keep track of your files and their history, 
and which enables you to do all the git things to the files in the working tree.

You do NOT have to interact with these directly.

Just know they are here

... and that people sometimes refer to the working tree AND the repository together 
as “The repository”...

Because we work hard on making life harder and more confusing than it needs to be



## Workspace/working tree
This is all the files and folders you would have if you did not use GIT.
It is folders, code files, headers, and build system files.

All the good stuff we want to work on.



## Index/Cache/Staging area

A single, large, binary file in the .git folder.

It keeps track of the differences between last time you saved, and how the
working tree is now. Every change, every new file, every file deleted.

You can think of it as the file git uses when you type
git status





# Merge conflicts tips

Git considers files that are in the middle of being merged as being staged
this means if you want to not accept incoming changes you can use
git restore --staged YOUR_FILE
to get rid of that file. Because git restore will not work.









# Basic workflow

This is a basic workflow you can copy.
It garantees that the main branch never have to do merge conflicts
It will work for a small study group or a large organisation

## Create a development branch

    git checkout <branch-you-want-to-update-maybe-master-or-main>
    git pull
    git checkout -b <your-branch-name>

## Develop your thing

    git diff <file-you-changed>
If the changes is what you expected then call
    git add <file-you-changed>
Repeat for all files you want added to the commit

    git commit -m "<message-explaining-why-you-made-these-changes>"
Repeat this entire step for as many times as it take for you to develop your thing



## Rebase your branch

### Make sure you have latest origin
    git checkout <branch-you-want-to-update-maybe-master-or-main>
    git pull

### Rebase your branch

    git checkout <your-branch-name>

    git pull origin <branch-you-want-to-update-maybe-master-or-main> --rebase
If there are merge conflics, solve them
Use
    git status
to help you know what to do
when you are done rebasing

### Merge the branches
    git checkout <branch-you-want-to-update-maybe-master-or-main>
Just for extra safety, we give the fast forward only, so if others have pushed into
master between when we pulled our merge will just fail
    git merge --ff-only <your-branch-name>
Done! :D

## Short version:

git checkout <branch-you-want-to-update-maybe-master-or-main>
git pull
git checkout -b <your-branch-name>

Make all your commits

git checkout <branch-you-want-to-update-maybe-master-or-main>
git pull
git checkout <your-branch-name>
git pull origin <branch-you-want-to-update-maybe-master-or-main> --rebase

git checkout <branch-you-want-to-update-maybe-master-or-main>
git merge --ff-only <your-branch-name>









# git on windows

## git working with paths longer than 260 characters on windows
Yes... we are doing this
So windows USED to have a 260 character path limit when using the windows API
Some programs use the old api. Git often being one of them

2 things need to be done to fix it.
First thing is to set the register to allow it
Second thing is to tell git that it needs to use this option.
I am informed that the reason this is off by default is that it can break things.
I have yet to see anyhting break, but now you know.

To do the two things, open a powershell with admin rights and run this:

Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Control\FileSystem -Name LongPathsEnabled


$MyPSexe = Get-Process -PID $PID | % Path
Start-Process -Verb RunAs $MyPSexe "-c","Set-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Control\FileSystem -Name LongPathsEnabled -Type DWord -Value 1"

Second thing is to set git to use it
in powershell, run this:
Start-Process -Verb RunAs "git" "config","--system","core.longpaths","true"




# github

Now, how to test that your everything works.
When you have a shell in a git repository folder you can type
git remote -v
This will show you the remotes you are pointing to.
Notice that these are the commands that requires authentication.
These will be "fetch" and "push"
Meaning, to test if everything works without having to modify your repository, you simply call
git fetch


## github on windows

I am... SO sorry...
But I will help. We will get through this

So. First things first

TODO explain SSH keys

TODO explain how to add keys to github

Now, this is all great, but git cannot find your keys
Because it does not know where to look for them.

So. 

We go to out user directory.
C:\Users\<Your user>

Here we create 3 files
One in the .ssh folder called "config"
In that one add this:

Host github.com
 Hostname github.com
 IdentityFile ~/.ssh/<filename of your PRIVATE SSH key>

Next one straight in the user directory called ".bash_profile"
Add this to the file:

test -f ~/.profile && . ~/.profile
test -f ~/.bashrc && . ~/.bashrc

And finally one straight in the user directory called ".bashrc" 
Where you add 

SSH_ENV="$HOME/.ssh/environment"

function run_ssh_env {
  . "${SSH_ENV}" > /dev/null
}

function start_ssh_agent {
  echo "Initializing new SSH agent..."
  ssh-agent | sed 's/^echo/#echo/' > "${SSH_ENV}"
  echo "succeeded"
  chmod 600 "${SSH_ENV}"

  run_ssh_env;

  ssh-add ~/.ssh/id_ed25519;
}

if [ -f "${SSH_ENV}" ]; then
  run_ssh_env;
  ps -ef | grep ${SSH_AGENT_PID} | grep ssh-agent$ > /dev/null || {
    start_ssh_agent;
  }
else
  start_ssh_agent;
fi



This info was found here: https://gist.github.com/bsara/5c4d90db3016814a3d2fe38d314f9c23


Now open up a new console, and git should work.