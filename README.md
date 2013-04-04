#git Cheat Sheet

#always pull from the same

    git config branch.master.remote origin
    git config branch.master.merge refs/heads/master

#Start from existing code (-u is to always push to the same)

    git remote add origin git@github.com:trufa/test.git
    git push -u origin master 

#Use kdiff3 as mergetool to solve conflicts

(paste this inside of your .git/config file)

    [merge]
        tool = kdiff3
    
    [mergetool "kdiff3"]
        path = C:/Program Files/KDiff3/kdiff3.exe
        keepBackup = false
        trustExitCode = false
        
#Three ways of undoing last n commits

[Read explanation here!](http://stackoverflow.com/a/6866485/463065)

You want to nuke commit your and never see it again.
    
    git reset --hard HEAD~n
    
You want to undo the commit but keep your changes
    
    git reset HEAD~n
    
Undo your commit but leave your files and your index:

    git reset --soft HEAD~n
