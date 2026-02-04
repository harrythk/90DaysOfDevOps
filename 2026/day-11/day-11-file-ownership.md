# Day 11 Challenge

## Files & Directories Created
ubuntu@ip-172-31-18-78:~$ ls -lR | grep "Feb  4"
drwxrwxr-x 2 berlin    heist-team 4096 Feb  4 06:21 app-logs
drwxrwxr-x 2 ubuntu    ubuntu     4096 Feb  4 06:56 bank-heist
-rw-rw-r-- 1 berlin    ubuntu        0 Feb  4 05:53 devops-file.txt
drwxrwxr-x 4 professor planners   4096 Feb  4 06:36 heist-project
-rw-rw-r-- 1 professor heist-team    0 Feb  4 06:16 project-config.yaml
-rw-rw-r-- 1 ubuntu    heist-team    0 Feb  4 06:02 team-notes.txt
-rw-rw-r-- 1 ubuntu ubuntu 0 Feb  4 06:56 access-codes.txt
-rw-rw-r-- 1 ubuntu ubuntu 0 Feb  4 06:56 blueprints.pdf
-rw-rw-r-- 1 ubuntu ubuntu 0 Feb  4 06:56 escape-plan.txt
drwxrwxr-x 2 professor planners 4096 Feb  4 06:37 plans
drwxrwxr-x 2 professor planners 4096 Feb  4 06:37 vault
-rw-rw-r-- 1 professor planners 0 Feb  4 06:37 strategy.conf
-rw-rw-r-- 1 professor planners 0 Feb  4 06:37 gold.txt

## Ownership Changes

- devops-file.txt: ubuntu:ubuntu → berlin:ubuntu
- team-notes.txt: ubuntu:ubuntu → ubuntu:heist-team
- project-config.yaml: ubuntu:ubuntu → professor:heist-team
- app-logs: ubuntu:ubuntu → berlin:heist-team
- vault: ubuntu:ubuntu → professor:planners
- plans: ubuntu:ubuntu → professor:planners
- gold.txt: ubuntu:ubuntu → professor:planners
- strategy.conf: ubuntu:ubuntu → professor:planners
- bank-heist: ubuntu:ubuntu → professor:planners
- access-codes.txt: ubuntu:ubuntu → tokyo:vault-team
- blueprints.pdf: ubuntu:ubuntu → berlin:tech-team
- escape-plan.txt: ubuntu:ubuntu → nairobi:vault-team 

ubuntu@ip-172-31-18-78:~$ ls -lR | grep "Feb  4"
drwxrwxr-x 2 berlin    heist-team 4096 Feb  4 06:21 app-logs
drwxrwxr-x 2 ubuntu    ubuntu     4096 Feb  4 06:56 bank-heist
-rw-rw-r-- 1 berlin    ubuntu        0 Feb  4 05:53 devops-file.txt
drwxrwxr-x 4 professor planners   4096 Feb  4 06:36 heist-project
-rw-rw-r-- 1 professor heist-team    0 Feb  4 06:16 project-config.yaml
-rw-rw-r-- 1 ubuntu    heist-team    0 Feb  4 06:02 team-notes.txt
-rw-rw-r-- 1 tokyo   vault-team 0 Feb  4 06:56 access-codes.txt
-rw-rw-r-- 1 berlin  tech-team  0 Feb  4 06:56 blueprints.pdf
-rw-rw-r-- 1 nairobi vault-team 0 Feb  4 06:56 escape-plan.txt
drwxrwxr-x 2 professor planners 4096 Feb  4 06:37 plans
drwxrwxr-x 2 professor planners 4096 Feb  4 06:37 vault
-rw-rw-r-- 1 professor planners 0 Feb  4 06:37 strategy.conf
-rw-rw-r-- 1 professor planners 0 Feb  4 06:37 gold.txt

## Commands Used
sudo chown berlin notes.txt
cat /etc/group
sudo chgrp -R developers hello.txt
ls -l hello.txt
touch devops-file.txt
sudo chown tokyo devops-file.txt
touch team-notes.txt
sudo groupadd heist-team
sudo chgrp heist-team team-notes.txt
ls -l | grep "Feb  4"
sudo chown professor:heist-team project-config.yaml
mkdir app-logs/
sudo chown berlin:heist-team app-logs/
mkdir -p heist-project/vault
mkdir -p heist-project/plans
touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
sudo groupadd planners
sudo chown -R professor:planners heist-project/
ls -lR heist-project/
sudo groupadd vault-team
sudo groupadd tech-team
sudo chown tokyo:vault-team bank-heist/access-codes.txt
sudo chown berlin:tech-team bank-heist/blueprints.pdf
sudo useradd -m nairobi -s /usr/bin/bash
sudo passwd nairobi
sudo chown nairobi:vault-team bank-heist/escape-plan.txt
ls -lR | grep "Feb  4"

## What I Learned
1. I learned how to modify user and group using command: sudo chown owner:group filename
2. Learned how to modify user and group recursively using command: sudo chown -R owner:group directory/
3. Learned how to use ls -l in better wau using recursively with -R and using grep to filter.
