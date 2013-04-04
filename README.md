#git Cheat Sheet

#always pull from the same

    git config branch.master.remote origin
    git config branch.master.merge refs/heads/master

#Start from existing code (-u is to always push to the same)

    git remote add origin git@github.com:trufa/test.git
    git push -u origin master 

#Use [kdiff3](http://kdiff3.sourceforge.net/) as mergetool to solve conflicts

(paste this inside of your .git/config file)

    [merge]
        tool = kdiff3
    
    [mergetool "kdiff3"]
        path = C:/Program Files/KDiff3/kdiff3.exe
        keepBackup = false
        trustExitCode = false
        
#Four ways of undoing last n commits

[Read explanation here!](http://stackoverflow.com/a/6866485/463065)

You want to nuke commit your and never see it again (Careful! Permanent loss).
    
    git reset --hard HEAD~n
    
You want to undo the commit but keep your changes
    
    git reset HEAD~n
    
Undo your commit but leave your files and your index:

    git reset --soft HEAD~n
    
If you only want to change the last commit message

    git commit --amend -m "New commit message"

#Basic branching [(tutorial)](http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Merging)

Checkout to a new branch

    git checkout -b newBranchName
    
Go back and merge

    git checkout master
    git merge newBranchName
