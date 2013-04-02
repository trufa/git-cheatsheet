git Cheat Sheet
==============

always pull from the same
==============
    git config branch.master.remote origin
    git config branch.master.merge refs/heads/master

Start from existing code (-u is to always push to the same)
==============
    git remote add origin git@github.com:trufa/test.git
    git push -u origin master 

Use kdiff3 as mergetool to solve conflicts
==============
(paste this inside of your .git/config file)
