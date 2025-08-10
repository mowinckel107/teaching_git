



# Table of Content:

1. [Often used Git commands](#Often-used-Git-commands)
    1. [To create a new branch](#To-create-a-new-branch)
    2. [To delete a remote branch](#To-delete-a-remote-branch)
    3. [To delete a local branch](#To-delete-a-local-branch)
    4. [To go back one local commit with files still being ready for commit](#To-go-back-one-local-commit-with-files-still-being-ready-for-commit)
    5. [When on feature branch rebase to sync it back up with master](#When-on-feature-branch-rebase-to-sync-it-back-up-with-master)
    6. [After pulling from a repo and it says “(new commits)”](#After-pulling-from-a-repo-and-it-says-“(new-commits)”)
    7. [To get the diff without having to scroll through it, use -P](#To-get-the-diff-without-having-to-scroll-through-it,-use--P)
    8. [Look at last commit](#Look-at-last-commit)
    9. [If you want to save output of a command](#If-you-want-to-save-output-of-a-command)
    10. [List all tags](#List-all-tags)
    11. [To temporarily hide your changes use](#To-temporarily-hide-your-changes-use)
    12. [show status, but only shows folders that are not tracked](#show-status,-but-only-shows-folders-that-are-not-tracked)
    13. [Show status of files not yet tracked](#Show-status-of-files-not-yet-tracked)
    14. [Get a list of all remote branches](#Get-a-list-of-all-remote-branches)
    15. [Show the entire command reply instead of using the pager](#Show-the-entire-command-reply-instead-of-using-the-pager)
    16. [To see what remote you are pointing to](#To-see-what-remote-you-are-pointing-to)
    17. [To change what remote you are pointing to](#To-change-what-remote-you-are-pointing-to)

2. [Git help syntax](#Git-help-syntax)

    1. [git commands are written in kebab case](#git-commands-are-written-in-kebab-case)
    2. [Angle brackets: <> means placeholder text](#Angle-brackets--means-placeholder-text)
    3. [Dash: -<a-letter> means single letter short form of an argument](#Dash--a-letter-means-single-letter-short-form-of-an-argument)
    4. [Double dash: --<word-or-words> is the long form of an argument](#Double-dash---word-or-words-is-the-long-form-of-an-argument)
    5. [Pipe: <option-1> | <option-2> means use either](#Pipe-option-1--option-2-means-use-either)
    6. [Square brackets: [] means an optional thing](#Square-brackets--means-an-optional-thing)

3. [Git term Definitions](#Git-term-Definitions)

    1. [Workspace/working tree](#Workspaceworking-tree)
    2. [Repository](#Repository)
    3. [Index/Cache/Staging area](#IndexCacheStaging-area)





**When your code is breaking at 2am**
**Git will save you!**

/o/
 O
||
__Gitman!__


# Often used Git commands

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

## Workspace/working tree
This is all the files and folders you would have if you did not use GIT.
It is folders, code files, headers, and build system files.

All the good stuff we want to work on.



## Repository

This is technically the hidden folder called “.git”.

It is all the files GIT uses to keep track of your files and their history, 
and which enables you to do all the git things to the files in the working tree.

You do NOT have to interact with these directly.

Just know they are here

... and that people sometimes refer to the working tree AND the repository together 
as “The repository”...

Because we work hard on making life harder and more confusing than it needs to be



## Index/Cache/Staging area

A single, large, binary file in the .git folder.

It keeps track of the differences between last time you saved, and how the
working tree is now. Every change, every new file, every file deleted.

You can think of it as the file git uses when you type
git status


