## Task 1: Your First Script
Create a file hello.sh
Add the shebang line #!/bin/bash at the top
Print Hello, DevOps! using echo
Make it executable and run it

#!/bin/bash
echo "Hello, Devops!"

ubuntu@ip-172-31-18-78:~/josh$ chmod +x hello.sh
ubuntu@ip-172-31-18-78:~/josh$ ./hello.sh
Hello, Devops!

## What happens if you remove the shebang line?
It still gives the expected output: Hello, Devops!

## Task 2: Variables

# Create variables.sh with:
A variable for your NAME
A variable for your ROLE (e.g., "DevOps Engineer")
Print: Hello, I am <NAME> and I am a <ROLE>

#!/bin/bash
NAME="Harendra"
ROLE="DevOps Engineer"
echo "Hello, I am $NAME and I am a $ROLE"

Output: Hello, I am Harendra and I am a DevOps Engineer

# Try using single quotes vs double quotes — what's the difference?
- When I used single quote the it didn't accept the value of variable and printed the line as it is:
  Hello, I am $NAME and I am a $ROLE
  While using double quotes, it accepted the variable value:
  Hello, I am Harendra and I am a DevOps Engineer


## Task 3: User Input with read

# Create greet.sh that:
Asks the user for their name using read
Asks for their favourite tool
Prints: Hello <name>, your favourite tool is <tool>

#!/bin/bash
read -p "Enter your name: " name
read -p "Enter your favourite tool: " tool
echo "Hello $name, your favourite tool is $tool"

Output:
Enter your name: Harendra
Enter your favourite tool: screwdriver
Hello Harendra, your favourite tool is screwdriver

## Task 4: If-Else Conditions

# Create check_number.sh that:
Takes a number using read
Prints whether it is positive, negative, or zero

#!/bin/bash

read -p "Enter the number you want to check: " NUMBER
if [ "$NUMBER" -gt 0 ]; then
        echo "$NUMBER is a positive number"
elif [ "$NUMBER" -lt 0 ]; then
        echo "$NUMBER is a negative number"
else
        echo "Zero"
fi

Output:
Enter the number you want to check: -5
-5 is a negative number

# Create file_check.sh that:
Asks for a filename
Checks if the file exists using -f
Prints appropriate message

#!/bin/bash

read -p "Enter the file name that you want to check: " FILE
if [ -f "$FILE" ]; then
        echo "File exist"
else
        echo "file doesn't exist"
fi

Output: 
Enter the file name that you want to check: file1.txt
File exist

## Task 5: Combine It All

# Create server_check.sh that:
Stores a service name in a variable (e.g., nginx, sshd)
Asks the user: "Do you want to check the status? (y/n)"
If y — runs systemctl status <service> and prints whether it's active or not
If n — prints "Skipped."

