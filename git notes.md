




When your code is breaking at 2am
GIT will save you!



# Definitions:

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


## index/cache/staging area

A single, large, binary file in the .git folder.

It keeps track of the differences between last time you saved, and how the working tree is now. Every change, every new file, every file deleted.



