## Task 1: For Loop

# 1. Create for_loop.sh that:
Loops through a list of 5 fruits and prints each one

#!/bin/bash
for i in apple banana grapes orange mango
do
        echo $i
done
echo "Done!"

# 2. Create count.sh that:
Prints numbers 1 to 10 using a for loop

#!/bin/bash

for i in {1..10}
do
        echo "$i"
done

## Task 2: While Loop

# 1. Create countdown.sh that:
Takes a number from the user
Counts down to 0 using a while loop
Prints "Done!" at the end

#!/bin/bash

read -p "Enter a number for reverse countdown: " num

while [ $num -gt 0 ]
do
        echo "$num"
        num='expr $num-1'
done


## Task 3: Command-Line Arguments

# 1. Create greet.sh that:
Accepts a name as $1
Prints Hello, <name>!
If no argument is passed, prints "Usage: ./greet.sh "

#!/bin/bash
echo "Hello, $1!"

ubuntu@ip-172-31-18-78:~/josh$ ./greet1.sh Harendra
Hello, Harendra!

# 2. Create args_demo.sh that:
Prints total number of arguments ($#)
Prints all arguments ($@)
Prints the script name ($0)

#!/bin/bash

echo "Total number of arguments: $#"
echo "All Arguments: $@"
echo "Script name is $0"

Output:
ubuntu@ip-172-31-18-78:~/josh$ ./args_demo.sh hello world how are you
Total number of arguments: 5
All Arguments: hello world how are you
Script name is ./args_demo.sh


## Task 4: Install Packages via Script

# Create install_packages.sh that:
Defines a list of packages: nginx, curl, wget
Loops through the list
Checks if each package is installed (use dpkg -s or rpm -q)
Installs it if missing, skips if already present
Prints status for each package


#!/bin/bash

if [ "$EUID" -ne 0 ]; then
        echo "Run as root"
        exit 1
fi

packages=(nginx curl wget)

apt-get update -y

for pkg in "${packages[@]}"
do
        if dpkg -s "$pkg" &>/dev/null 2>&1; then
                echo ""$pkg" is already installed"
        else
                echo "Installing package $pkg"
                apt install $pkg -y
        fi
done

Output:

root@ip-172-31-18-78:~# cd /home/ubuntu/josh/
root@ip-172-31-18-78:/home/ubuntu/josh# ./install_packages.sh
Hit:1 http://eu-west-1.ec2.archive.ubuntu.com/ubuntu noble InRelease
Get:2 http://eu-west-1.ec2.archive.ubuntu.com/ubuntu noble-updates InRelease [126 kB]
Hit:3 http://eu-west-1.ec2.archive.ubuntu.com/ubuntu noble-backports InRelease
Hit:4 http://security.ubuntu.com/ubuntu noble-security InRelease
Get:5 http://eu-west-1.ec2.archive.ubuntu.com/ubuntu noble-updates/main amd64 Packages [1740 kB]
Fetched 1866 kB in 1s (2790 kB/s)
Reading package lists... Done
nginx is already installed
curl is already installed
wget is already installed


## Task 5: Error Handling

# Create safe_script.sh that:
Uses set -e at the top (exit on error)
Tries to create a directory /tmp/devops-test
Tries to navigate into it
Creates a file inside
Uses || operator to print an error if any step fails

#!/bin/bash

#set -e

mkdir /tmp/devops-test || echo "Directory already exists"
cd /tmp/devops-test
touch new-file.txt || echo "The file was not created"

Output:
ubuntu@ip-172-31-18-78:~/josh$ ./safe_script.sh
mkdir: cannot create directory ‘/tmp/devops-test’: File exists
Directory already exists
























