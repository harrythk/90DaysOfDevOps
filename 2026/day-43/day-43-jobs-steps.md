## Task 1: Multi-Job Workflow
# Create .github/workflows/multi-job.yml with 3 jobs:

build — prints "Building the app"
test — prints "Running tests"
deploy — prints "Deploying"
# Make test run only after build succeeds. Make deploy run only after test succeeds.

name: Multiple jobs

on:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Print App Building
        run: echo "Building the app"
  
  test:
    needs: [build]
    runs-on: ubuntu-latest
    steps:
      - name: Print Running Tests
        run: echo "Running Tests"
  
  deploy:
    needs: [test]
    runs-on: ubuntu-latest
    steps:
      - name: Print Deploying
        run: echo "Deploying"

# Check the workflow graph in the Actions tab — does it show the dependency chain?

<img width="676" height="248" alt="image" src="https://github.com/user-attachments/assets/f238915a-8bbb-4ad8-8e36-32fa5c19ca74" />

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 2: Environment Variables
# In a new workflow, use environment variables at 3 levels:

Workflow level — APP_NAME: myapp
Job level — ENVIRONMENT: staging
Step level — VERSION: 1.0.0
# Print all three in a single step and verify each is accessible.

<img width="340" height="204" alt="image" src="https://github.com/user-attachments/assets/55984007-9ed1-46a5-9a7a-0ac1b3f9d339" />

# Then use a GitHub context variable — print the commit SHA and the actor (who triggered the run).

name: Environment Veriable Tests

on:
  workflow_dispatch:
env:
  APP_NAME: myapp

jobs:
  varibales:
    
    runs-on: ubuntu-latest
    env:
      ENVIRONMENT: staging

    steps:
      - name: Print Environment varibales
        env:
          VERSION: 1.0.0
        run: |
          echo $APP_NAME
          echo $ENVIRONMENT
          echo $VERSION
          echo "commit SHA: ${{ github.sha }}"
          echo "the actor: ${{ github.actor }}"

<img width="434" height="218" alt="image" src="https://github.com/user-attachments/assets/9678b3ae-770b-45e7-b825-47bbe6392c21" />

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 3: Job Outputs
# Create a job that sets an output — e.g., today's date as a string
# Create a second job that reads that output and prints it
# Pass the value using outputs: and needs.<job>.outputs.<name>

name: Job Outputs

on:
  workflow_dispatch:

jobs:
  date-string:
    runs-on: ubuntu-latest
    outputs:
      date: ${{ steps.set_date.outputs.date }}
    steps:
      - name: Setting Outputs
        id: set_date
        run: |
          echo "date=$(date)" >> $GITHUB_OUTPUT
  
  read-outputs:
    needs: [date-string]
    runs-on: ubuntu-latest
    steps:
      - name: Reading Outputs
        run: |
          echo "Output date: ${{ needs.date-string.outputs.date }}"

<img width="422" height="197" alt="image" src="https://github.com/user-attachments/assets/9ddc8c10-02ca-4682-80bf-e4f1a39c7053" />

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 4: Conditionals
In a workflow, add:

# A step that only runs when the branch is main
# A step that only runs when the previous step failed
# A job that only runs on push events, not on pull requests
# A step with continue-on-error: true — what does this do?

name: Conditionals Test

on:
  push:
  pull_request:

jobs:
  conditionaals:
    runs-on: ubuntu-latest

    steps:
      - name: Runs when branch is main
        if: github.ref == 'refs/heads/main'
        run: echo "The current branch name is ${{ github.ref_name }}"
      
      - name: Intentional failure step
        run: exit 1
        continue-on-error: true
      
      - name: Runs when previous step fail
        if: failure()
        run: echo "Previous step failed"
  
  push-event:
    if: github.event_name == 'push'
    runs-on: ubuntu-latest
    steps:
      - name: run on push event
        run: echo "There was a push event then this job is running."
      
      - name: Continuation step
        run: |
          echo "This step will fail"
          exit 1
        continue-on-error: true
      
      - name: Step after error
        run: echo "Workflow continued even after failure"

  <img width="560" height="365" alt="image" src="https://github.com/user-attachments/assets/c20c0ff9-7507-4b7e-a686-6075c7a4b356" />

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 5: Putting It Together
# Create .github/workflows/smart-pipeline.yml that:

Triggers on push to any branch
Has a lint job and a test job running in parallel
Has a summary job that runs after both, prints whether it's a main branch push or a feature branch push, and prints the commit message

--------------------------------

name: Smart Pipeline

on:
  push:
    branches:
      - '**'

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - name: Code Checkout
        uses: actions/checkout@v4
      
      - name: Lint step
        run: echo "Running Lint"
  
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Code Checkout
        uses: actions/checkout@v4
      
      - name: Test Step
        run: echo "Running Tests"
  
  summary:
    needs: [lint, test]
    runs-on: ubuntu-latest

    steps:
      - name: Print branch name
        run: |
          if ["${{ github.ref_name }}" = "main"]; then
            echo "This is push to the main branch."
          else
            echo "This is push to the feature branch: ${{ github.ref_name }}"
          fi
      
      - name: Print Commit message
        run: |
          echo "Commit message: ${{ github.event.commits[0].message }}"


<img width="948" height="382" alt="image" src="https://github.com/user-attachments/assets/91f428cc-6c1c-4e2d-9c7e-d0fa1cd80df8" />


<img width="547" height="259" alt="image" src="https://github.com/user-attachments/assets/11d67527-1504-471c-a327-a84863c02d7d" />








