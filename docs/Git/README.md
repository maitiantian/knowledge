# Git Cheat Sheet

### CREATE
|description|usage|
|:---|:---|
|Clone an existing repository|$ git clone ssh://user@domain.com/repo.git|
|Create a new local repository|$ git init|

### LOCAL CHANGES
|description|usage|
|:---|:---|
|Changed files in your working directory|$ git status|
|Changes to tracked files|$ git diff|
|Add all current changes to the next commit|$ git add .|
|Add some changes in &lt;file&gt; to the next commit|$ git add -p &lt;file&gt;|
|Commit all local changes in tracked files|$ git commit -a|
|Commit previously staged changes|$ git commit|
|Change the last commit. Don't amend published commits!|$ git commit --amend|

### COMMIT HISTORY
|description|usage|
|:---|:---|
|Show all commits, starting with newest|$ git log|
|Show changes over time for a specifc file|$ git log -p &lt;file&gt;|
|Who changed what and when in &lt;file&gt;|$ git blame &lt;file&gt;|

### BRANCHES & TAGS
|description|usage|
|:---|:---|
|List all existing branches|$ git branch -av|
|Switch HEAD branch|$ git checkout &lt;branch&gt;
|Create a new branch based on your current HEAD|$ git branch &lt;new-branch&gt;|
|Create a new tracking branch based on a remote branch|$ git checkout --track &lt;remote/branch&gt;|
|Delete a local branch|$ git branch -d &lt;branch&gt;
|Mark the current commit with a tag|$ git tag &lt;tag-name&gt;|

### UPDATE & PUBLISH
|description|usage|
|:---|:---|
|List all currently confgured remotes|$ git remote -v|
|Show information about a remote|$ git remote show &lt;remote&gt;|
|Add new remote repository, named &lt;remote&gt;|$ git remote add &lt;shortname&gt; &lt;url&gt;|
|Download all changes from &lt;remote&gt;, but don't integrate into HEAD|$ git fetch &lt;remote&gt;|
|Download changes and directly merge/integrate into HEAD|$ git pull &lt;remote&gt; &lt;branch&gt;|
|Publish local changes on a remote|$ git push &lt;remote&gt; &lt;branch&gt;|
|Delete a branch on the remote|$ git branch -dr &lt;remote/branch&gt;|
|Publish your tags|$ git push --tags|

### MERGE & REBASE
|description|usage|
|:---|:---|
|Merge &lt;branch&gt; into your current HEAD|$ git merge &lt;branch&gt;|
|Rebase your current HEAD onto &lt;branch&gt;. Don't rebase published commits!|$ git rebase &lt;branch&gt;|
|Abort a rebase|$ git rebase --abort|
|Continue a rebase after resolving conﬂicts|$ git rebase --continue|
|Use your confgured merge tool to solve conﬂicts|$ git mergetool|
|Use your editor to manually solve conﬂicts and (after resolving) mark file as resolved|$ git add &lt;resolved-file&gt;|
| |$ git rm &lt;resolved-file&gt;|

### UNDO
|description|usage|
|:---|:---|
|Discard all local changes in your working directory|$ git reset --hard HEAD|
|Discard local changes in a specifc file|$ git checkout HEAD &lt;file&gt;|
|Revert a commit (by producing a new commit with contrary changes)|$ git revert &lt;commit&gt;|
|Reset your HEAD pointer to a previous commit …and discard all changes since then|$ git reset --hard &lt;commit&gt;|
|…and preserve all changes as unstaged changes|$ git reset &lt;commit&gt;|
|…and preserve uncommitted local changes|$ git reset --keep &lt;commit&gt;|

