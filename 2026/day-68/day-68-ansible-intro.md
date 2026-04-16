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

# Task 3: Install Ansible

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





