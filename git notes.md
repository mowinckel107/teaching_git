

# Table of Content:

 1. [Often used Git commands](#Often-used-Git-commands)
    1. [git init](#git-init)
    2. [git clone](#git-clone)
    3. [git status](#git-status)
    4. [git remote](#git-remote)
    5. [git fetch](#git-fetch)
    6. [git pull](#git-pull)
    7. [git push](#git-push)
    8. [git reset](#git-reset)
    9. [git diff](#git-diff)
   10. [git log](#git-log)
   11. [git tag](#git-tag)
   12. [git stash](#git-stash)
   13. [git branch](#git-branch)
   14. [git config](#git-config)
   15. [git rebase](#git-rebase)
   16. [git merge](#git-merge)
   17. [git submodule](#git-submodule)
   18. [Save command output to file](#Save-command-output-to-file)
 2. [Weird git behavior and how to solve it](#Weird-git-behavior-and-how-to-solve-it)
    1. [git cannot detect changes in file names between high and low case](#git-cannot-detect-changes-in-file-names-between-high-and-low-case)
    2. [Restore empty working tree](#Restore-empty-working-tree)
 3. [Git help syntax explanation](#Git-help-syntax-explanation)
    1. [git commands are written in kebab case](#git-commands-are-written-in-kebab-case)
    2. [Angle brackets: <> means placeholder text](#Angle-brackets--means-placeholder-text)
    3. [Dash: -<a-letter> means single letter short form of an argument](#Dash--a-letter-means-single-letter-short-form-of-an-argument)
    4. [Double dash: --<word-or-words> is the long form of an argument](#Double-dash---word-or-words-is-the-long-form-of-an-argument)
    5. [Pipe: <option-1> | <option-2> means use either](#Pipe-option-1--option-2-means-use-either)
    6. [Square brackets: [] means an optional thing](#Square-brackets--means-an-optional-thing)
    7. [double dashes alone: [--] means done with options](#double-dashes-alone----means-done-with-options)
 4. [Git terms definitions](#Git-terms-definitions)
    1. [Repository](#Repository)
    2. [Workspace/working tree](#Workspaceworking-tree)
    3. [Index/Cache/Staging area](#IndexCacheStaging-area)
    4. [Fast forward](#Fast-forward)
    5. [origin/<branch>](#originbranch)
 5. [Merge conflicts tips](#Merge-conflicts-tips)
 6. [Basic workflow](#Basic-workflow)
    1. [Create a development branch](#Create-a-development-branch)
    2. [Develop your thing](#Develop-your-thing)
    3. [Rebase your branch](#Rebase-your-branch)
       1. [Make sure you have latest origin](#Make-sure-you-have-latest-origin)
       2. [Rebase your branch](#Rebase-your-branch)
       3. [Merge the branches](#Merge-the-branches)
    4. [Short version](#Short-version)
 7. [git on windows](#git-on-windows)
    1. [git working with paths longer than 260 characters on windows](#git-working-with-paths-longer-than-260-characters-on-windows)
 8. [github](#github)
    1. [github on windows](#github-on-windows)
  
  
  
  
  
**When your code is breaking at 2am**  
**Git will save you!**  
  
What have I changed?  
When did this happen?  
Who did this?  
Why is this like this?  
  
**gitman will save you!**  
  
/o/  
 O  
||  
__Gitman!__  
  
  
  
  
  
# Often used Git commands  
These are in an order so if you read from top to bottom you get all the info you need
and will learn of the commands in the order where they are most useful  



## git init  
to turn a project into a git repository:  
Have your shell in the projects root folder and use:  
```  
git init  
```  
Thats it.  
  
Now you can use it locally with  
```  
git add <your-file>  
```  
and  
```  
git commit -m "<your-commit-message>"  
```  
If you ever want it on a remote repo like github then see the "git remote" headline :)  
  
## git clone  
To clone into differently named folder  
```  
git clone <git-repo-url>  <different-named-folder>  
```  
  
notice that you can also clone from local repositories:  
```  
git clone <git-repo-path> <different-named-folder>  
```  
  
if you want to make a local fake remote:  
```  
git clone --bare <git-repo-url> <fake-remote-folder>  
```  
  
  
##  git status  
show status, but only shows folders that are not tracked:  
```  
git status  
```  
Show status of files not yet tracked:  
```  
git status -u  
```  
  
  
## git remote  
To see what remote you are pointing to  
```  
git remote -v  
```  
  
To change what remote you are pointing to  
```  
git remote set-url origin <the-new-origin>  
```  
  
if the repository never had a remote, ie, was created by  
```  
git init  
```  
  
You first get the new remote url by creating the repository on the remote  
Then get the url you would normally clone it with  
Then use that url like so:  
```  
git remote add origin <repository-url>  
```  
and then simply  
```  
git push  
```  
which may prompt you to call  
```  
git push --set-upstream origin <your-branch-name>  
```  
  
Remove a remote with  
```  
git remote remove origin  
```  
  
  
## git fetch  
This commands gets the latest info from the remote WITHOUT changing your working tree  
Can be really handy if you are confused about what is happening, especially followed by  
git status  
fetch NEVER changes anything, so it is always safe to use  
  
  
## git pull  
This calls fetch, and then it tries to take all the remotes changes and put them into  
your local  
If this can be fast forwarded, it will happen with no further input from you.  
If it cannot, git will ask you what it should do.  
  
This is because git will NEVER do anything destructive without you telling it to.  
Meaning that while commands may change things, you can ALWAYS get back to where you were.  
But sometimes it is nessesary to use git pull in a destructive way. For example changing  
past commits. Then you have to use the force flag like so:  
```  
git pull --force  
```  
or  
```  
git pull -f  
```  
  
  
## git push  
This does the equivilient of the remote calling "git pull" on your local  
  
  
If you are doing this to a central branch like main or master, you can ensure it  
either goes well, or git aborts and do not do any changes by calling  
```  
git push --ff-only  
```  
  
  
## git reset  
To go back one local commit with files still being ready for commit  
```  
git reset --soft HEAD~1  
```  
to also remove the staged files, use --hard instead  
  
If you then want the remote to also go back one commit then  
```  
git push -f  
```  
  
  
## git diff  
To get the diff without having to scroll through it:  
```  
git -P diff <absolute-path-to-file>  
```  
This can also be handled permanently by git config  
  
To compare a file between 2 commits  
```  
git diff <commit-id-1> <commit-id-2> <file-you-want-to-compare>  
```  
  
To find when file was added  
```  
git log --diff-filter=A -- <your-file.txt>  
```  
  
To highlight words instead of lines with diff:  
```  
git diff --word-diff <The-file>  
```  
  
  
## git log  
To look at last commit:  
```  
git log --name-status HEAD^..HEAD  
```  
  
  
##  git tag  
To list all tags:  
```  
git tag -l *  
```  
Note that you can modify the wildcard to be more specific.  
  
  
  
## git stash  
To temporarily hide your changes:  
```  
git stash  
```  
and  
```  
git stash pop  
```  
  
  
To see all saved stashes:  
```  
git stash list  
```  
  
To delete all saved stashes:  
```  
git stash clear  
```  
  
  
## git branch  
To get a list of all remote branches:  
```  
git branch -r  
```  
  
To create a new branch  
```  
git checkout -b <branch-name>  
```  
  
To delete a local branch  
```  
git branch -d <old-branch>  
```  
  
To delete a remote branch  
```  
git push origin -d <branch-name>  
```  
  
  
  
  
  
## git config  
git config interacts with the configuration of git.  
There is a global configuration file and one for each repo  
Local changes overrules global ones  
  
local configs is changed with  
  
git config <name-of-configuration> <what-to-set-configuration-to>  
  
and global with  
  
git config --global <name-of-configuration> <what-to-set-configuration-to>  
  
  
The most normal setting to set is your name and email  
that will show up in your git commits  
These are set like so:  
```  
git config --global user.name <your-name>  
```  
and  
```  
git config --global user.email <your-email>  
  
```  
  
  
To show the entire command reply instead of using the pager  
```  
git config --global core.pager "cat"  
```  
This is equivalent to starting a command with “git -P”  
  
If you always want to use an argument in a command, you can automate that by using an alias  
an example of making an alias so  
```  
git df  
```  
actually calls  
```  
git diff --word-diff  
```  
  
```  
git config --global alias.df "diff --word-diff"  
```  
  
  
## git rebase  
When on feature branch rebase to sync it back up with master  
```  
    git pull origin master --rebase  
    git push -f  
```  
(If commits have been squashed then simply type “git rebase --continue” until you have skipped all your commits that are in fact in the squashed commit)  
  
  
  
## git merge  
When on master how to merge a branch into master  
To tell git to fail and stop if everything is not 100% fine, add the fast forward only argument  
```  
git merge --ff-only <your-development-branch-name>  
```  
  
  
## git submodule  
After pulling from a repo and it says “(new commits)”  
That is because the sub-modules are not automatically pulled when the main one is. Fix this with the command:  
```  
git submodule update --init --recursive  
```  
  
To do the equivilent of "pull" for all submodules recursively:  
```  
git submodule update --remote  
```  
  
To change a submodule to a branch  
```  
git config -f .gitmodules submodule.<submodule-name>.branch <name-of-a-branch>  
```  
  
  
## Save command output to file  
```  
git blame file.name > output.txt  
```  
or  
```  
git log -p -- filename > output.txt  
```  
  
  
  
  
# Weird git behavior and how to solve it  
  
## git cannot detect changes in file names between high and low case  
You poke git to detect it with  
```  
git mv <Source> <Destination>  
```  
for example:  
```  
git mv <my-lower-case-named-file> <my-upper-case-named-file>  
```  
  
## Restore empty working tree:  
```  
git commit -m'for now'  
git checkout -f  
git reset --soft HEAD~1  
```  
  
  
  
  
# Git help syntax explanation  
  
## git commands are written in kebab case  
Meaning replacing spaces with dashes  
so a command might look like this:  
```  
git my-weird-command  
```  
  
  
  
## Angle brackets: <> means placeholder text  
so  
```  
git a-weird-command <path-to-file>  
```  
  
could be called like  
```  
git a-weird-command "/home/moose/Desktop/teaching_git/git notes.md"  
```  
notice I put the path in quotations because it have spaces.  
This is to avoid git thinking it is 3 different argument  
  
  
  
## Dash: -<a-letter> means single letter short form of an argument  
For example, the short for for help in the git command is  
```  
git -h  
```  
  
  
  
## Double dash: --<word-or-words> is the long form of an argument  
for example  
```  
git --help  
```  
  
  
  
## Pipe: <option-1> | <option-2> means use either  
so a git command  
```  
git weirdest-command --create-fartbucket | --fill-bucket-with-fart  
```  
could be called like this:  
```  
git weirdest-command --create-fartbucket  
```  
or like this:  
```  
git weirdest-command --fill-bucket-with-fart  
```  
And would do the same thing  
  
  
## Square brackets: [] means an optional thing  
so  
```  
git weird [<path>] <author>  
```  
could be called  
```  
git weird moose  
```  
or  
```  
git weird "/home/moose/Desktop/teaching_git/git notes.md" moose  
```  
  
This can also show up in the argument explanations  
so for example if you write  
```  
git show -h  
```  
one of the output lines looks like this:  
```  
-q, --[no-]quiet      suppress diff output  
```  
  
meaning you can write  
```  
git show --quiet  
```  
to run the command quiet  
or  
```  
git show --no-quiet  
```  
to run the command NOT quiet :3  
  
  
  
## double dashes alone: [--] means done with options  
This is to fix when it is not possible for git to distinguish when the options are done  
and the following arguments start.  
so if you have (for some reason) named a file "main" and you have a branch called "main"  
now you want to revert changes to that file and call  
```  
git checkout main  
```  
git... now defaults to switching to the branch main  
so if you want to revert the changes you call it like this  
```  
git checkout -- main  
```  
and it works! :D  
  
  
  
  
  
# Git terms definitions  
  
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
```    
git status  
```  
  
  
## Fast forward  
This refers to when you call  
```  
git pull  
```  
or  
```  
git push  
```  
And the only difference between the branch that is recieving changes and the branch  
giving changes is that the giving branch have more commits.  
Then git is able to merge the branches with "fast forward". Meaning easily without  
changing any other commit in the branch  
  
  
## origin/<branch>  
"origin" means this is the remote your own local branch is pointing to  
Note, as always, that this is how things looked last time git checked the remote  
git is NOT permanently connected to the remote. Only when you ask it to update  
  
  
  
  
  
# Merge conflicts tips  
  
Git considers files that are in the middle of being merged as being staged  
this means if you want to not accept incoming changes you can use  
```  
git restore --staged <your-file>  
```  
to get rid of that file. Because git restore will not work.  
  
  
  
  
  
  
  
  
  
# Basic workflow  
  
This is a basic workflow you can copy.  
It garantees that the main branch never have to do merge conflicts  
It will work for a small study group or a large organisation  
  
## Create a development branch  
```  
    git checkout <branch-you-want-to-update-maybe-master-or-main>  
    git pull  
    git checkout -b <your-branch-name>  
```  
  
## Develop your thing  
```  
    git diff <file-you-changed>  
```  
If the changes is what you expected then call  
```  
git add <file-you-changed>  
```  
Repeat for all files you want added to the commit  
```  
git commit -m "<message-explaining-why-you-made-these-changes>"  
```  
Repeat this entire step for as many times as it take for you to develop your thing  
  
  
  
## Rebase your branch  
  
### Make sure you have latest origin  
```  
git checkout <branch-you-want-to-update-maybe-master-or-main>  
git pull  
```  
### Rebase your branch  
```  
git checkout <your-branch-name>  
git pull origin <branch-you-want-to-update-maybe-master-or-main> --rebase  
```  
If there are merge conflics, solve them  
Use  
```  
git status  
```  
to help you know what to do  
when you are done rebasing  
  
### Merge the branches  
```  
git checkout <branch-you-want-to-update-maybe-master-or-main>  
```  
Just for extra safety, we give the fast forward only, so if others have pushed into  
master between when we pulled our merge will just fail  
```  
git merge --ff-only <your-branch-name>  
```  
Done! :D  
  
## Short version:  
```  
git checkout <branch-you-want-to-update-maybe-master-or-main>  
git pull  
git checkout -b <your-branch-name>  
```  
Make all your commits  
```  
git checkout <branch-you-want-to-update-maybe-master-or-main>  
git pull  
git checkout <your-branch-name>  
git pull origin <branch-you-want-to-update-maybe-master-or-main> --rebase  
```  
```  
git checkout <branch-you-want-to-update-maybe-master-or-main>  
git merge --ff-only <your-branch-name>  
```  
  
  
  
  
  
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
```  
git remote -v  
```  
This will show you the remotes you are pointing to.  
Notice that these are the commands that requires authentication.  
These will be "fetch" and "push"  
Meaning, to test if everything works without having to modify your repository, you simply call  
```  
git fetch  
```  
  
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
C:\Users\<Your-user>  
  
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
