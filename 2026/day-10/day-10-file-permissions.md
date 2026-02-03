# Day 10 Challenge

## Files Created
-rw-rw-r-- 1 ubuntu ubuntu    0 Feb  3 06:06 devops.txt
-rw-rw-r-- 1 ubuntu ubuntu   41 Feb  3 06:10 notes.txt
-rw-rw-r-- 1 ubuntu ubuntu   20 Feb  3 06:13 script.sh

## Understand Permissions

Currently User and group has permission to read and write, while others have permision of read only for 3 newly created files.  

## Permission Changes
sudo chmod 764 script.sh
sudo chmod 444 devops.txt
sudo chmod 640 notes.txt
mkdir -m 755 project

## Test Permissions
echo "test line" > devops.txt
-bash: devops.txt: Permission denied

sudo chmod 664 script.sh
./script.sh
-bash: ./script.sh: Permission denied

## Commands Used
touch devops.txt
cat > notes.txt
vim script.sh

cat notes.txt
vim script.sh
head -n 5 /etc/passwd
tail -n 5 /etc/passwd

ls -l | grep 'script'
sudo chmod 764 script.sh
./script.sh
sudo chmod 444 devops.txt
mkdir -m 755 project
