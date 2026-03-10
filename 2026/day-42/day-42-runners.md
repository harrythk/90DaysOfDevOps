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
















