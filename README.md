#git Cheat Sheet

###always pull from the same
    git config branch.master.remote origin
    git config branch.master.merge refs/heads/master

###Start from existing code (-u is to always push to the same)

    git remote add origin git@github.com:trufa/test.git
    git push -u origin master 

###Use [kdiff3](http://kdiff3.sourceforge.net/) as mergetool to solve conflicts

(paste this inside of your .git/config file)

    [merge]
        tool = kdiff3
    
    [mergetool "kdiff3"]
        path = C:/Program Files/KDiff3/kdiff3.exe
        keepBackup = false
        trustExitCode = false
        
###Four ways of undoing last n commits

[Read explanation here!](http://stackoverflow.com/a/6866485/463065)

You want to nuke commit your and never see it again (Careful! Permanent loss).
    
    git reset --hard HEAD~n
    
You want to undo the commit but keep your changes
    
    git reset HEAD~n
    
Undo your commit but leave your files and your index:

    git reset --soft HEAD~n
    
If you only want to change the last commit message

    git commit --amend -m "New commit message"

###Retrieve a specific version of a file

    git show <commit-id>:<path>

###Basic branching [(tutorial)](http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Merging)

Checkout to a new branch

    git checkout -b newBranchName
    
Go back and merge

    git checkout master
    git merge newBranchName

###Help for resolve merge conflicts

When at a merge conflict, find changes between the common ancestor and
the file on our branch which was merged

    git diff :1:<path> :2:<path>

Find changes between the common ancestor and the file on the branch we
are merging into the current branch

    git diff :1:<path> :3:<path>

###Revert uncommited file to last version

    git checkout filename
    
###Set vimdiff as default difftool [(source)](http://stackoverflow.com/a/3713865/463065)

    git config --global diff.tool vimdiff
    git config --global difftool.prompt false
    git config --global alias.d difftool

###Stash local changes to be able to pull without errors [(source)](http://stackoverflow.com/a/14318266/463065)

    git stash save --keep-index

###Remove untracked files

Files are lost permanently. Use *-n* or *--dry-run* to preview the effected files.

####Remove only untracked files

    git clean -f

####Remove untracked files & directories

    git clean -f -d

###Check if there is anything to pull, bring remote up to date [(source)](http://stackoverflow.com/a/3278427/463065)

    git remote update
    
###Know what you pulled [(source)](http://stackoverflow.com/a/1362990/463065)

    git diff master master@{1}
    
###Checkout to a remote branch

    git checkout -b abranch origin/abranch

###Move uncommitted changes to a new branch [(source)](http://stackoverflow.com/a/1394804/463065)

    git checkout -b <new-branch>
    git add <files>
    git commit
    
###Move uncommitted changes to existing branch [(source)](http://stackoverflow.com/a/556986/463065)

    git stash
    git checkout branch2
    git stash pop

###Get commits by certain user [(source)](http://stackoverflow.com/a/2954501/463065)

    git log --author=<pattern>
    
###Rename a file

    git mv dir/oldName dir/newName

And commit the changes.

Note: the file needs to be added (`git add file`).

###Exclude file from diff [(source)](http://stackoverflow.com/a/10421385/463065)

Create a repository specific diff driver with this command

    git config diff.nodiff.command /bin/true

or for all your repos with --global.

Assign the nodiff driver to those files you want ignored in your `.git/info/attributes` file.

    irrelevant.php    diff=nodiff
    
###See what was changed by one specific commit

    git show HashOfTheCommmit

###See history of one file [(source)](http://stackoverflow.com/questions/278192/view-the-change-history-of-a-file-using-git-versioning)

    gitk fileName
    
Or

    git log -p fileName

###List changes between two branches

List changes files

    git diff --name-status firstBranch secondBranch

List changed files and number of changes

    git diff --stat --color firstBranch secondBranch

List changed commits in one branch but not another (in secondBranch not in firstBranch).

    git log --oneline ^firstBranch secondBranch

###Tags (annotated, the kind you can push to another repo)

Make an annotated tag

    git tag -a -m "Tag for 1.2.3.4 release" release-1.2.3.4

Push an annotate tag to another repo

    git push origin release-1.2.3.4

or push all tags

    git push --tags origin

Rename a tag in local and remote repo

    git tag newTagName oldTagName
    git tag -d oldTagName
    git push origin :refs/tags/oldTagName
    git push --tags

###Repo splunking

List files in the repo on abranch (use 'HEAD' for current branch)

    git ls-tree --full-tree -r abranch | awk '{print $4}'
