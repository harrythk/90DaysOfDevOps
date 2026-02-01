# Day 09 Challenge

## Users & Groups Created
Users-
tokyo:x:1002:1002::/home/tokyo:/usr/bin/bash
berlin:x:1001:1001::/home/berlin:/usr/bin/bash
professor:x:1003:1004::/home/professor:/usr/bin/bash

Groups-
developers:x:1005:tokyo,berlin
admins:x:1006:berlin,professor

## Group Assignments
developers:x:1005:tokyo,berlin
admins:x:1006:berlin,professor

## Directories Created
drwxrwxr-x 2 root developers 4096 Feb  1 14:47 /opt/dev-project/

Files created by berlin and tokyo in dev-project
-rw-rw-r-- 1 berlin berlin 0 Feb  1 14:47 berlin-file.txt
-rw-rw-r-- 1 tokyo  tokyo  0 Feb  1 14:46 tokyo-file.txt

## Commands Used
sudo useradd -m berlin -s /usr/bin/bash
sudo useradd -m tokyo -s /usr/bin/bash
sudo useradd -m professor -s /usr/bin/bash
cat /etc/passwd

sudo groupadd developers
sudo groupadd admins
sudo usermod -aG developers tokyo
sudo usermod -aG developers,admins berlin
cat /etc/group

sudo mkdir /opt/dev-project
sudo chgrp developers /opt/dev-project/

su tokyo
su berlin

sudo chmod 775 dev-project
ls -l
getent group
ls -ld /opt/dev-project/

## What I Learned
1. I learned the command to assign a user to one or more groups using command: usermod -aG <groups> <user>
2. Learned how to change group ownership of a directory using command: chgrp <group> <diectory path>
3. Learned how to change permissions of a group for user, group and others using command: chmod
