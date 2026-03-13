## Task 1: GitHub Secrets
Go to your repo → Settings → Secrets and Variables → Actions
Create a secret called MY_SECRET_MESSAGE
## Create a workflow that reads it and prints: The secret is set: true (never print the actual value)
## Try to print ${{ secrets.MY_SECRET_MESSAGE }} directly — what does GitHub show?

name: Secret reading 

on:
  workflow_dispatch:

jobs:
  Secret-scan:
    runs-on: ubuntu-latest
    steps:
      - name: Checking secret message
        run: |
          if [ -n "${{ secrets.MY_SECRET_MESSAGE }}" ]; then
            echo "The secret is set: true"
          else
            echo "The secret is set: false"
          fi
      
      - name: print secret message
        run: |
            echo "${{ secrets.MY_SECRET_MESSAGE }}"

<img width="653" height="364" alt="image" src="https://github.com/user-attachments/assets/cc8e69b6-c8be-4b8a-bbdc-2c2db572746a" />

## Why should you never print secrets in CI logs?
Doing so can expose your credentials to other who can expolit your pipeline.

+++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 2: Use Secrets as Environment Variables
Pass a secret to a step as an environment variable
Use it in a shell command without ever hardcoding it
Add DOCKER_USERNAME and DOCKER_TOKEN as secrets (you'll need these on Day 45)

name: Docker Login Test

on:
  workflow_dispatch

jobs:
  docker-login:
    runs-on: ubuntu-latest
    steps:
      - name: Docker login check using secrets
        env:
          DOCKER_USERNAME: ${{ vars.DOCKER_USERNAME }}
          DOCKER_TOKEN: ${{ secrets.DOCKER_TOKEN }}
        run: |
          echo "$DOCKER_TOKEN" | docker login \
          --username "$DOCKER_USERNAME" \
          --password-stdin


<img width="1860" height="717" alt="image" src="https://github.com/user-attachments/assets/7f68e691-0bf5-4aac-8ee4-5c1d3238e7a2" />


+++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 3: Upload Artifacts
Create a step that generates a file — e.g., a test report or a log file
Use actions/upload-artifact to save it
After the workflow runs, download the artifact from the Actions tab

name: Artifact generate and download

on:
  workflow_dispatch:

jobs:
  artifact-generate:
    runs-on: ubuntu-latest
    steps:
      - name: Code Checkout
        uses: actions/checkout@v4

      - name: generating a report
        run: |
          mkdir -p Reports
          echo "Test result summary" >> Reports/test.log
          ls -la >> Reports/test.log
      
      - name: downloading report
        uses: actions/upload-artifact@v4
        with:
          name: test-report
          path: Reports/test.log


<img width="1871" height="655" alt="image" src="https://github.com/user-attachments/assets/97e5c984-a084-4e05-8e10-d1764cd82a10" />


+++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 4: Download Artifacts Between Jobs
Job 1: generate a file and upload it as an artifact
Job 2: download the artifact from Job 1 and use it (print its contents)





















