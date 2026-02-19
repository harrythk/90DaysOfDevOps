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
 
 
