# Task 1: Understand Ansible

## What is configuration management? Why do we need it?
Configuration Management is the process of managing and mainitaing a remote system or server. It helps us deploying new softwares, maintaining configuration etc. on remote servers.
We need this to avoide manual works which ensure faster deployement and make sure that consitency is maintained.

## How is Ansible different from Chef, Puppet, and Salt?
Ansible is agentless and push based while all others have agent instelled on the nodes and uses pull method to get status from master node for configuration.

## What does "agentless" mean? How does Ansible connect to managed nodes?
Agentless means that Ansible doesn't have agents installed on the nodes which help manage the state of configurations on node servers. Ansible connects with nodes using SSH.

## Draw or describe the Ansible architecture:
<img width="246" height="194" alt="image" src="https://github.com/user-attachments/assets/4472dab7-6c3f-4969-bbb9-6812d07f0807" />


++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 3: Install Ansible

[ec2-user@ip-172-31-30-142 ~]$ ansible --version
ansible [core 2.15.3]
  config file = /home/ec2-user/ansible.cfg
  configured module search path = ['/home/ec2-user/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3.9/site-packages/ansible
  ansible collection location = /home/ec2-user/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/bin/ansible
  python version = 3.9.25 (main, Dec 10 2025, 00:00:00) [GCC 11.5.0 20240719 (Red Hat 11.5.0-5)] (/usr/bin/python3.9)
  jinja version = 3.1.4
  libyaml = True

## On which machine did you install Ansible? Why is it only needed on the control node? 
Installed Ansible on my local machine. The local machine can SSH into all the nodes and manage those nodes.

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
# Task 4: Create Your Inventory File

## ansible all -i inventory.ini -m ping

<img width="778" height="388" alt="image" src="https://github.com/user-attachments/assets/998a2d63-a584-4ac4-bee5-d505911a3135" />

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 5: Run Ad-Hoc Commands

## ansible all -i inventory.ini -m command -a "uptime"

<img width="784" height="215" alt="image" src="https://github.com/user-attachments/assets/210d1c26-a425-4158-ae59-a8dcfb7a2f39" />

## ansible web -i inventory.ini -m command -a "free -h"

<img width="778" height="109" alt="image" src="https://github.com/user-attachments/assets/92981bad-f7ea-4d39-952a-04e9e0deb1db" />

## ansible all -i inventory.ini -m command -a "df -h"

<img width="502" height="317" alt="image" src="https://github.com/user-attachments/assets/1f746747-58a4-40fc-a8e3-cd0fba988d2a" />

## ansible web -i inventory.ini -m yum -a "name=git state=present" --become

<img width="739" height="184" alt="image" src="https://github.com/user-attachments/assets/2d5e3ecc-56c2-4dbb-89f9-636198ed80c1" />

## echo "Hello from Ansible" > hello.txt
ansible all -i inventory.ini -m copy -a "src=hello.txt dest=/tmp/hello.txt"

<img width="763" height="446" alt="image" src="https://github.com/user-attachments/assets/1dba7276-0490-49e7-afb0-936c726fc51a" />

## ansible all -i inventory.ini -m command -a "cat /tmp/hello.txt"

<img width="755" height="116" alt="image" src="https://github.com/user-attachments/assets/321d9a83-6b71-48f0-bbe3-65af3e35fd1a" />

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 6: Explore Inventory Groups and Patterns

## ansible application -i inventory.ini -m ping

<img width="740" height="166" alt="image" src="https://github.com/user-attachments/assets/cd06d924-c0be-4c36-a6ed-6dfc0d7299d6" />

## ansible db -i inventory.ini -m ping  

<img width="395" height="89" alt="image" src="https://github.com/user-attachments/assets/8694fe74-4a5a-48cb-9645-b15dc8a37ccb" />

## ansible all_servers -i inventory.ini -m ping 

<img width="751" height="243" alt="image" src="https://github.com/user-attachments/assets/ff6997bc-35e6-41c6-a664-aeb89ddc8922" />

## ansible 'web:app' -i inventory.ini -m ping

<img width="745" height="167" alt="image" src="https://github.com/user-attachments/assets/b2e4ce74-fc53-4805-b89d-d41e5a2525fa" />

## ansible 'all:!db' -i inventory.ini -m ping

<img width="758" height="167" alt="image" src="https://github.com/user-attachments/assets/96f14170-c1aa-4119-9f05-a90f47bba689" />

## ansible all -m ping

It worked without specifying the inventory file.
<img width="508" height="268" alt="image" src="https://github.com/user-attachments/assets/bc278af9-b5d4-46a3-9b85-e0f47b5d18ca" />

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Difference between command and shell modules

Command module runs command directly abd can run simple commands.
Shell module is run via shell and is used when complex shell logic is required.
