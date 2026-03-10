# Task 1: GitHub-Hosted Runners

## Create a workflow with 3 jobs, each on a different OS:
ubuntu-latest
windows-latest
macos-latest
In each job, print:
The OS name
The runner's hostname
The current user running the job
## Watch all 3 run in parallel

name: Github Hosted Runner Test

on:
  push: 
    branches: [main]

jobs:
  Linux:
    runs-on: ubuntu-latest
    steps:
      - name: Print OS name
        run: cat /etc/os-release
      
      - name: Print runner hostname
        run: hostname
      
      - name: Show current user
        run: whoami
  
  Windows:
    runs-on: windows-latest
    steps:
      - name: Print OS name
        run: echo ${{ runner.os }}
      
      - name: Print runner hostname
        run: hostname
      
      - name: Show current user
        run: whoami
  
  Macos:
    runs-on: macos-latest
    steps:
      - name: Print OS name
        run: sw_vers
      
      - name: Print runner hostname
        run: hostname
      
      - name: Show current user
        run: whoami

<img width="525" height="233" alt="image" src="https://github.com/user-attachments/assets/76f2a740-9e04-4330-b242-27e83d46cc2b" />

## What is a GitHub-hosted runner? Who manages it?
A GitHub-hosted runner is a virtual machine (VM) provided by GitHub that runs your workflow jobs in GitHub Actions. This fully managed by github.

++++++++++++++++++++++++++++++++++++++++++++++++++++


# Task 2: Explore What's Pre-installed
## On the ubuntu-latest runner, run a step that prints:
Docker version
Python version
Node version
Git version

- name: Check version of intalled tools
  run: |
    docker --version
    python3 --version
    node --version
    git --version

<img width="379" height="268" alt="image" src="https://github.com/user-attachments/assets/77b00c4d-b51d-4ffa-ace7-86a40be64307" />

## Why does it matter that runners come with tools pre-installed?
It matters that runners come with tools pre-installed because it makes your CI/CD workflows faster and simpler. If the tools are alreday installed, you don't need to install then everytime you run a workflow.


++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 3: Set Up a Self-Hosted Runner

## Go to your GitHub repo → Settings → Actions → Runners → New self-hosted runner
Choose Linux as the OS
Follow the instructions to download and configure the runner on:
Your local machine, OR
A cloud VM (EC2, Utho, or any VPS)
## Start the runner — verify it shows as Idle in GitHub
## Verify: Your runner appears in the Runners list with a green dot.


<img width="569" height="193" alt="image" src="https://github.com/user-attachments/assets/7294d841-25a9-4936-893d-7c97e0a6a8fd" />


++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 4: Use Your Self-Hosted Runner

## Create .github/workflows/self-hosted.yml
Set runs-on: self-hosted
Add steps that:
## Print the hostname of the machine (it should be YOUR machine/VM)
## Print the working directory
## Create a file and verify it exists on your machine after the run
## Trigger it and watch it run on your own hardware

name: Self Hosted Runner

on:
  push:
    branches: [main]

jobs:
  self-host:
    runs-on: self-hosted
    steps:
      - name: Print hostname of machine
        run: hostname
      
      - name: Print working directory
        run: pwd
      
      - name: Create a file
        run: touch testfile.txt

ubuntu@ip-172-31-47-89:~/actions-runner-repo2/_work/new-github-actions-practice/new-github-actions-practice$ ls
testfile.txt


++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 5: Labels
# Add a label to your self-hosted runner (e.g., my-linux-runner)

<img width="410" height="89" alt="image" src="https://github.com/user-attachments/assets/faf5cdc5-7d36-48d4-981e-1ec1bbdfda86" />

# Update your workflow to use runs-on: [self-hosted, my-linux-runner]

jobs:
  self-host:
    runs-on: [self-hosted, my-linux-runner]

# Trigger it — does it still pick up the job?

<img width="514" height="194" alt="image" src="https://github.com/user-attachments/assets/d5f14a5b-a545-46da-a46d-5c6e7cc70908" />

# Why are labels useful when you have multiple self-hosted runners?

Labels (tags) are very useful when you have multiple self-hosted runners in GitHub Actions because they allow workflows to select the correct machine for a job.
Without labels, GitHub might send a job to any available runner, which can cause failures if the machine doesn’t have the required tools.

++++++++++++++++++++++++++++++++++++++++++++++++++++


## Task 6: GitHub-Hosted vs Self-Hosted
Fill this in your notes:

<img width="244" height="134" alt="image" src="https://github.com/user-attachments/assets/bce809a5-bd81-47f8-823b-ef5978d6ac6b" />

















