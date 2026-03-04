## Task 1: Set Up

# Create a new public GitHub repository called github-actions-practice
# Clone it locally
harry@NEW4090-G8:~/practice-github-action$ git clone git@github.com:harrythk/github-actions-practice.git

# Create the folder structure: .github/workflows/
harry@NEW4090-G8:~/practice-github-action/github-actions-practice$ mkdir -p .github/workflows

+++++++++++++++++++++++++++++++++++++++++++++++++

## Task 2: Hello Workflow

# Create .github/workflows/hello.yml with a workflow that:

Triggers on every push
Has one job called greet
Runs on ubuntu-latest
Has two steps:
Step 1: Check out the code using actions/checkout
Step 2: Print Hello from GitHub Actions!

# hello.yml file >
name: hello

on:
  push:
    branches: [main]

jobs:
  greet:
    runs-on: ubuntu-latest
    steps:
      - name: Check out the code using actions/checkout
        uses: actions/checkout@v4

      - name: Print hello
        run: echo "Hello from GitHub Actions!" 

# Push it. Go to the Actions tab on GitHub and watch it run.
# Verify: Is it green? Click into the job and read every step.

<img width="495" height="246" alt="image" src="https://github.com/user-attachments/assets/ec08b07f-99d2-45cd-a3a7-c9e35709c89e" />

+++++++++++++++++++++++++++++++++++++++++++++++++

## Task 3: Understand the Anatomy

# Look at your workflow file and write in your notes what each key does:

on: This triggers the workflow when code is pushed.
jobs: Defines one or more jobs in the workflow.
runs-on: Defines which machine (ubuntu-latest) the job runs on.
steps: A list of actions performed inside the greet job.
uses: Used to run a prebuilt action created by github
run: Executes a shell command on the runner.
name: This is just a display label shown in the Actions UI.

+++++++++++++++++++++++++++++++++++++++++++++++++

## Task 4: Add More Steps
Update hello.yml to also:

# Print the current date and time
- name: current date and time
  run: date "+%Y-%m-%d %H:%M:%S"

# Print the name of the branch that triggered the run (hint: GitHub provides this as a variable)
- name: branch name
  run: echo "name of branch that triggered the run is ${{ github.ref_name }}"

# List the files in the repo
- name: list of files
  run: ls -a

# Print the runner's operating system
- name: runner's operating system
  run: uname -a 

# Push again — watch the new run.

<img width="627" height="445" alt="image" src="https://github.com/user-attachments/assets/ff4e45c2-e01b-4cd1-816c-2b45a873132f" />

+++++++++++++++++++++++++++++++++++++++++++++++++

## Task 5: Break It On Purpose

# Add a step that runs a command that will fail (e.g., exit 1 or a misspelled command)

- name: misspelled command
  run: misspelledcommand

# Push and observe what happens in the Actions tab

<img width="500" height="305" alt="image" src="https://github.com/user-attachments/assets/9e178b7e-ce86-4f9d-84ab-995b4c7fc579" />

# Fix it and push again

<img width="518" height="233" alt="image" src="https://github.com/user-attachments/assets/90d220cf-8fa3-4990-a7ef-f46054be8da0" />






