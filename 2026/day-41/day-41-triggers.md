## Task 1: Trigger on Pull Request

# Create .github/workflows/pr-check.yml
# Trigger it only when a pull request is opened or updated against main
# Add a step that prints: PR check running for branch: <branch name>

name: PR Check

on:
  pull_request:
    branches: [main]

jobs:
  branch-name:
    runs-on: ubuntu-latest
    steps:
      - name: Print PR branch name
        run: echo "PR check running for branch is ${{ github.head_ref }}"

# Create a new branch, push a commit, and open a PR
# Watch the workflow run automatically

<img width="506" height="214" alt="image" src="https://github.com/user-attachments/assets/afe97768-5040-469f-9fea-2cccd37c40ca" />

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 2: Scheduled Trigger
# Add a schedule: trigger to any workflow using cron syntax
# Set it to run every day at midnight UTC

on:

  schedule:
    - corn: "0 0 * * *"
