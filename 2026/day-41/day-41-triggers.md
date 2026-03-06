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

# What is the cron expression for every Monday at 9 AM?
corn: "0 23 * * 1"

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


## Task 3: Manual Trigger
# Create .github/workflows/manual.yml with a workflow_dispatch: trigger
# Add an input that asks for an environment name (staging/production)
# Print the input value in a step

name: manual trigger

on:
  workflow_dispatch:
    inputs:
      environment:
        description: 'Enter environment (staging/production)'
        required: true
        options:
          - staging
          - production

jobs:
  input-value:
    runs-on: ubuntu-latest
    steps:
      - name: Print environment input
        run: echo "Selected environment is ${{github.event.inputs.environment}}"


# Go to the Actions tab → find the workflow → click Run workflow

<img width="517" height="230" alt="image" src="https://github.com/user-attachments/assets/9834a22b-0334-4669-802e-8b7af650dbb8" />

# Verify: Can you trigger it manually and see your input printed?
Yes, I was able to trigger it manually and input was printed as well.

<img width="377" height="199" alt="image" src="https://github.com/user-attachments/assets/f4a3b2ec-4b96-4454-bffb-de6bf43e364f" />


+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


## Task 4: Matrix Builds

# Create .github/workflows/matrix.yml that:

# Uses a matrix strategy to run the same job across:
# Python versions: 3.10, 3.11, 3.12
# Each job installs Python and prints the version

name: matrix

on:
  push:
    branches: [main]

jobs:
  install-print:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        python-version: ["3.10", "3.11", "3.12"]
    
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
      
      - name: install python
        uses: actions/setup-python@v5
        with:
          python-version: ${{matrix.python-version}}
      
      - name: Print Python version
        run: python --version


# Watch all 3 run in parallel

<img width="532" height="245" alt="image" src="https://github.com/user-attachments/assets/1e2df696-c23a-486d-924b-01516aa84125" />

# Then extend the matrix to also include 2 operating systems — how many total jobs run now?
5 jobs run now.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++














