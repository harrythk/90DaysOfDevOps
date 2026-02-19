## Task 1: Understanding Branches

# What is a branch in Git?
Branch is a separate line of development in git like main, dev, staging etc.

# Why do we use branches instead of committing everything to main?
Branches help make sure that whatever changes made doesn't go to production directly

# What is HEAD in Git?
HEAD tells you latest commit on that branch.

# What happens to your files when you switch branches?
When you switch branch it shows the data in the file as per last update in that particular branch.

==========================================================================================================================

## Task 2: Branching Commands — Hands-On
In your devops-git-practice repo, perform the following:

# List all branches in your repo
ubuntu@ip-172-31-18-78:~/devops-git-practice$ git branch
* master
	
# Create a new branch called feature-1
ubuntu@ip-172-31-18-78:~/devops-git-practice$ git branch feature-1

# Switch to feature-1
ubuntu@ip-172-31-18-78:~/devops-git-practice$ git switch feature-1
Switched to a new branch 'feature-1'

# Create a new branch and switch to it in a single command — call it feature-2
ubuntu@ip-172-31-18-78:~/devops-git-practice$ git checkout -b feature-2
Switched to a new branch 'feature-2'

# Try using git switch to move between branches — how is it different from git checkout?
ubuntu@ip-172-31-18-78:~/devops-git-practice$ git switch feature-1
Switched to branch 'feature-1'

Git switch is used to switch between branches only.
Git checkout can do multiple things like switching between branches, creating new branch, checking specific commit etc.

# Make a commit on feature-1 that does not exist on main

ubuntu@ip-172-31-18-78:~/devops-git-practice$ git log --oneline
9b1ee96 (HEAD -> feature-1) feat: added additional command
17094d4 (master, feature-2) feat: adding new commands
d867923 feat: new commit with additional descriptions
adb6038 Feat: added description to commands
9baafb1 initial commit

# Switch back to main — verify that the commit from feature-1 is not there

ubuntu@ip-172-31-18-78:~/devops-git-practice$ git log --oneline
17094d4 (HEAD -> master, feature-2) feat: adding new commands
d867923 feat: new commit with additional descriptions
adb6038 Feat: added description to commands
9baafb1 initial commit

# Delete a branch you no longer need
ubuntu@ip-172-31-18-78:~/devops-git-practice$ git branch -d feature-2
Deleted branch feature-2 (was 17094d4).

==========================================================================================================================

## Task 3: Push to GitHub

# Create a new repository on GitHub (do NOT initialize it with a README)
# Connect your local devops-git-practice repo to the GitHub remote

ubuntu@ip-172-31-18-78:~/devops-git-practice$ git remote add origin git@github.com:harrythk/devops-git-practice-repo.git

# Push your main branch to GitHub
ubuntu@ip-172-31-18-78:~/devops-git-practice$ git push origin main
Enumerating objects: 12, done.
Counting objects: 100% (12/12), done.
Delta compression using up to 2 threads
Compressing objects: 100% (8/8), done.
Writing objects: 100% (12/12), 1.39 KiB | 1.39 MiB/s, done.
Total 12 (delta 3), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (3/3), done.
To github.com:harrythk/devops-git-practice-repo.git
 * [new branch]      main -> main


# Push feature-1 branch to GitHub
ubuntu@ip-172-31-18-78:~/devops-git-practice$ git push origin feature-1
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 2 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 361 bytes | 361.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote:
remote: Create a pull request for 'feature-1' on GitHub by visiting:
remote:      https://github.com/harrythk/devops-git-practice-repo/pull/new/feature-1
remote:
To github.com:harrythk/devops-git-practice-repo.git
 * [new branch]      feature-1 -> feature-1

# What is the difference between origin and upstream?
Origin - default name of the remote repository
upstream - repository from where yu fork in your github

==========================================================================================================================

# What is the difference between git fetch and git pull?
git fetch - this commad fetch new commits from remote. But, doesn't update files.
git pull - this command fetch new commits and make changes to the file as well.


==========================================================================================================================

# Clone any public repository from GitHub to your local machine

ubuntu@ip-172-31-18-78:~/devops-git-practice$ git clone git@github.com:harrythk/Shell-scripts.git
Cloning into 'Shell-scripts'...
remote: Enumerating objects: 10, done.
remote: Counting objects: 100% (10/10), done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 10 (delta 1), reused 10 (delta 1), pack-reused 0 (from 0)
Receiving objects: 100% (10/10), done.
Resolving deltas: 100% (1/1), done.

# Fork the same repository on GitHub, then clone your fork

ubuntu@ip-172-31-18-78:~/devops-git-practice$ git clone git@github.com:harrythk/python-for-devops.git
Cloning into 'python-for-devops'...
remote: Enumerating objects: 83, done.
remote: Counting objects: 100% (34/34), done.
remote: Compressing objects: 100% (33/33), done.
remote: Total 83 (delta 9), reused 1 (delta 1), pack-reused 49 (from 1)
Receiving objects: 100% (83/83), 24.77 KiB | 528.00 KiB/s, done.
Resolving deltas: 100% (16/16), done.

# What is the difference between clone and fork?
Clone = makes a local copy of a repository on your machine
Fork = makes your own copy of someone else’s repository on GitHub.

# When would you clone vs fork?
I will use clone when i have to bring files from remote to may local repo.
I will use fork when I have to get a copy of repository from others repo to my github repo, nothing in local.

# After forking, how do you keep your fork in sync with the original repo?
We need to use sync fork > update branch


























