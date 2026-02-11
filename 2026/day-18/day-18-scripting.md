## Task 1: Basic Functions

# Create functions.sh with:
A function greet that takes a name as argument and prints Hello, <name>!
A function add that takes two numbers and prints their sum
Call both functions from the script
+++++++++++++++++++++++++++++++++++++++++++++++++

#!/bin/bash

greet() {
echo "Hello, $1!"
}

add() {
        sum=$(($num1 + $num2))
        echo "Sum is: $sum"
}

greet "$1"

read -p "Enter the first number for addition " num1
read -p "Enter the second number for addition " num2

add "$num1" "$num2"

OUTPUT:
ubuntu@ip-172-31-18-78:~/josh$ ./functions.sh Harendra
Hello, Harendra!
Enter the first number for addition 7
Enter the second number for addition 9
Sum is: 16
+++++++++++++++++++++++++++++++++++++++++++++++++

## Task 2: Functions with Return Values

#Create disk_check.sh with:
A function check_disk that checks disk usage of / using df -h
A function check_memory that checks free memory using free -h
A main section that calls both and prints the results

+++++++++++++++++++++++++++++++++++++++++++++++++++

#!/bin/bash

check_disk() {
        df -h | awk 'NR<=2'
}

check_memory() {
        free -h | awk 'NR==1,NR==2'
}

echo "Available disk space: "
check_disk
echo "Available memory: "
check_memory

OUTPUT:
Available disk space:
Filesystem       Size  Used Avail Use% Mounted on
/dev/root        6.8G  2.8G  4.0G  41% /
Available memory:
               total        used        free      shared  buff/cache   available
Mem:           914Mi       344Mi       549Mi       2.7Mi       174Mi       569Mi

+++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 3: Strict Mode — set -euo pipefail

#Create strict_demo.sh with set -euo pipefail at the top
Try using an undefined variable — what happens with set -u?
Try a command that fails — what happens with set -e?
Try a piped command where one part fails — what happens with set -o pipefail?

#!/bin/bash
set -euo pipefail

echo "*********Testing set -u***********"

echo "Hello $name"

echo "This line won't print as script will exit"


echo "*********Testing set -e***********"

cd /unavailable_direcory

echo "This line won't print as script will exit"

echo "**********Testing set -o pipefail**************

echo "apple" | grep "abcd"

echo "This line won't print as pipefail is active"

# Document: What does each flag do?

set -e → protects from undefined variables
set -u → stops script when a command fails
set -o pipefail → catches pipe failures

++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 4: Local Variables

# Create local_demo.sh with:
A function that uses local keyword for variables
Show that local variables don't leak outside the function
Compare with a function that uses regular variables


#!/bin/bash
name="Global name" # Global variable
local_name() {

        local name="Local Name"
        echo "Inside the funtion local_name: $name"
}

echo "Befor calling the function: name = $name"
echo "Calling funtion"
local_name

OUTPUT:
Befor calling the function: name = Global name
Calling funtion
Inside the funtion local_name: Local Name

++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 5: Build a Script — System Info Reporter

# A function to print hostname and OS info
A function to print uptime
A function to print disk usage (top 5 by size)
A function to print memory usage
A function to print top 5 CPU-consuming processes
A main function that calls all of the above with section headers
Use set -euo pipefail at the top
Output should look clean and readable.


#!/bin/bash
set -euo pipefail

hostname_OS_info() {
        echo "==============================="
        echo "Hostname: $(hostname)"
        echo "OS Info: "
        cat /etc/os-release | awk 'NR==2,NR==3'

}

system_uptime() {
        echo "==============================="
        echo "Uptime of system: "
        uptime | awk '{print $1, $2, $3}'
}

disk_usage() {
        echo "==============================="
        echo " Top 5 Disk Usage (Root Level): "
        du -ah | sort -rh | head -n 5
}

memory_usage() {
        echo "==============================="
        echo " Memory Usage: "
        free -h | awk 'NR==1,NR==2'
}

CPU_usage() {
        echo "==============================="
        echo " Top 5 CPU Consuming Processes: "
        ps aux --sort=-%cpu | head -n 6
}

main() {
        echo "++++++SYSTEM HEALTH REPORT++++++++"
        hostname_OS_info

        system_uptime

        disk_usage

        memory_usage

        CPU_usage

        echo "+++++++END OF REPORT++++++++++"
}

main "$@"


OUTPUT:

++++++SYSTEM HEALTH REPORT++++++++
===============================
Hostname: ip-172-31-18-78
OS Info:
NAME="Ubuntu"
VERSION_ID="24.04"
===============================
Uptime of system:
20:00:25 up 7:45,
===============================
 Top 5 Disk Usage (Root Level):
104K    .
8.0K    ./scripts
8.0K    ./batch10
4.0K    ./variables.sh
4.0K    ./tesh.sh
===============================
 Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           914Mi       351Mi       542Mi       2.7Mi       174Mi       562Mi
===============================
 Top 5 CPU Consuming Processes:
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         612  0.0  2.4 1802028 23140 ?       Ssl  12:14   0:15 /usr/bin/containerd
ubuntu      2159  0.0  0.5  14992  4860 ?        S    16:55   0:03 sshd: ubuntu@pts/2
root          53  0.0  0.0      0     0 ?        S    12:14   0:06 [kswapd0]
root         782  0.0  3.3 1898340 30904 ?       Ssl  12:14   0:04 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
root           1  0.0  1.1  22252 10560 ?        Ss   12:14   0:03 /sbin/init


++++++++++++++++++++++++++++++++++++++++++++++++++++++

What you learned (3 key points)
- Learned writing production level scripts to monitor server
- How to catch errors early by stopping the script on undefined variables, command failures, or pipeline failures.
- Local variable usage









