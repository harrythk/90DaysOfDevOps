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

