## Task 1: Git Merge — Hands-On

# Create a new branch feature-login from main, add a couple of commits to it
ubuntu@ip-172-31-18-78:~/devops-git-practice$ git checkout -b feature-login
Switched to a new branch 'feature-login'

ubuntu@ip-172-31-18-78:~/devops-git-practice$ git commit -m "Init: added a new file"
[feature-login 0eca873] Init: added a new file
 1 file changed, 1 insertion(+)
 create mode 100644 login.txt

# Switch back to main and merge feature-login into main
ubuntu@ip-172-31-18-78:~/devops-git-practice$ git merge feature-login
Updating aaec442..0eca873
Fast-forward
 login.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 login.txt

# Observe the merge — did Git do a fast-forward merge or a merge commit?
Git did a fast-forward merge

# Now create another branch feature-signup, add commits to it — but also add a commit to main before merging
ubuntu@ip-172-31-18-78:~/devops-git-practice$ git checkout -b feature-signup
Switched to a new branch 'feature-signup'

# Merge feature-signup into main — what happens this time?
ubuntu@ip-172-31-18-78:~/devops-git-practice$ git merge feature-signup
Auto-merging git-commands.md
Merge made by the 'ort' strategy.
 git-commands.md | 1 +
 1 file changed, 1 insertion(+)

This time ort stategy was used to merge and this time merge commit happened.

# What is a fast-forward merge? 
Git command moves the pointer to latest commit of the other branch.

# When does Git create a merge commit instead?
when both branches have different commits, then merge commit happens.

# What is a merge conflict? (try creating one intentionally by editing the same line in both branches)
A merge conflict happens when Git cannot automatically decide which changes to keep while merging two branches. This happens when same file and line are edited.

========================================================================================================================================================================================

## Task 2: Git Rebase — Hands-On
Create a branch feature-dashboard from main, add 2-3 commits
While on main, add a new commit (so main moves ahead)
Switch to feature-dashboard and rebase it onto main
Observe your git log --oneline --graph --all — how does the history look compared to a merge?

ubuntu@ip-172-31-18-78:~/devops-git-practice$ git log --oneline --graph --all
* 9a9b061 (HEAD) after removing conflict
* f850974 (main) test commit
| * d66cacf (feature-dashboard) second commit for dashboard
| * b82ab00 firt commit for dashboard
| *   f13f489 (feature-signup) removed conflict
| |\
| |/
|/|
* | 7fcfb62 feat: added a new command
* |   afa0131 Merge branch 'feature-signup'
|\ \
* | | 0bc89d4 feat: added a viewing command
* | | 6414481 feat: added a command with long description
| | * 62bd9ed featf: added a new command as main
| |/
| * 7dd9af9 feat - added cherry picking command
|/
* 7e1fd7f feat: added 1 new command
* 0eca873 (feature-login) Init: added a new file
* aaec442 Update git commands
* f022f26 (origin/main) Update git-commands.md
| * 9b1ee96 (origin/feature-1, feature-1) feat: added additional command
|/
* 17094d4 feat: adding new commands
* d867923 feat: new commit with additional descriptions
* adb6038 Feat: added description to commands
* 9baafb1 initial commit

# What does rebase actually do to your commits?
Rebase takes your feature branch commits and replays them on top of another branch, creating new commits and rewriting history to produce a cleaner linear commit graph.

# How is the history different from a merge?
A merge preserves branch history and creates a merge commit, while rebase rewrites commits and creates a linear history without a merge commit.

# Why should you never rebase commits that have been pushed and shared with others?
Because rebase rewrites commit history, and rewriting shared history breaks other developer repositories.

# When would you use rebase vs merge?
Use rebase to keep a clean linear history when working on local branches. Use merge when working on shared branches to keep history intact.

========================================================================================================================================================================================



















