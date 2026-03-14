## Task 1: Prepare
Use the app you Dockerized on Day 36 (or any simple Dockerfile)
Add the Dockerfile to your github-actions-practice repo (or create a minimal one)
Make sure DOCKER_USERNAME and DOCKER_TOKEN secrets are set from Day 44

Used a new app from github: sample-dockerize-django

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 2: Build the Docker Image in CI
Create .github/workflows/docker-publish.yml that:

# Triggers on push to main
# Checks out the code
# Builds the Docker image and tags it

name: docker build and push

on:
  push:
    branches: [main]

jobs:
  build-and-push:
    runs-on: ubuntu-latest
    steps:
      - name: checkout code
        uses: actions/checkout@v4
      
      - name: build image and tag
        uses: docker/build-push-action@v6
        with:
          context: .
          push: false
          load: true
          tags: |
            ${{ vars.DOCKER_USERNAME }}/github-actions-new-app:latest

<img width="1844" height="655" alt="image" src="https://github.com/user-attachments/assets/c363f6f9-ea8e-409b-8058-9afee38e1f28" />

<img width="1855" height="869" alt="image" src="https://github.com/user-attachments/assets/aee177a6-c48f-495b-8442-5e5899d5519f" />


+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 3: Push to Docker Hub
Add steps to:

# Log in to Docker Hub using your secrets
# Tag the image as username/repo:latest and also username/repo:sha-<short-commit-hash>
# Push both tags

name: docker build and push

on:
  push:
    branches: [main]

jobs:
  build-and-push:
    runs-on: ubuntu-latest
    steps:
      - name: checkout code
        uses: actions/checkout@v4
      
      - name: login dockerhub
        uses: docker/login-action@v3
        with:
          username: ${{ vars.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_TOKEN }}
      
      - name: build image and tag
        uses: docker/build-push-action@v6
        with:
          context: .
          push: true
          load: true
          tags: |
            ${{ vars.DOCKER_USERNAME }}/github-actions-new-app:latest
            ${{ vars.DOCKER_USERNAME }}/github-actions-new-app:${{ github.sha }}

<img width="938" height="642" alt="image" src="https://github.com/user-attachments/assets/72ae5d64-b54c-4b12-af84-3cfbfaefe3d8" />

Link to dockerhub repo: https://hub.docker.com/repository/docker/harrythk/github-actions-new-app/general
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 4: Only Push on Main
# Add a condition so the push step only runs on the main branch — not on feature branches or PRs.

Test it: push to a feature branch and verify the image is built but NOT pushed.

name: build image and push
        if: ${{ github.ref == 'refs/heads/main' }}
        uses: docker/build-push-action@v6
        with:
          context: .
          push: true
          tags: |
            ${{ vars.DOCKER_USERNAME }}/github-actions-new-app:latest
            ${{ vars.DOCKER_USERNAME }}/github-actions-new-app:${{ github.sha }}

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


# Task 5: Add a Status Badge
Get the badge URL for your docker-publish workflow from the Actions tab
Add it to your README.md
Push — the badge should show green

<img width="1884" height="692" alt="image" src="https://github.com/user-attachments/assets/0bce8cde-4857-43f5-8f87-881c1f45a23e" />

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


# Task 6: Pull and Run It
# On your local machine (or a cloud server), pull the image you just pushed

harry@NEW4090-G8:~/new-github-actions-practice$ docker pull harrythk/github-actions-new-app:latest

harry@NEW4090-G8:~/new-github-actions-practice$ docker images
                                                                                                                 i Info →   U  In Use
IMAGE                                    ID             DISK USAGE   CONTENT SIZE   EXTRA
alpine:latest                            25109184c71b       13.1MB         3.95MB        
entrypoint-test:latest                   09fc546edb66         13MB         3.86MB        
harrythk/github-actions-new-app:latest   fd0cce810a3a       1.73GB          447MB 

# Run it
# Confirm it works

harry@NEW4090-G8:~/new-github-actions-practice$ docker run -d -p 8000:8000 harrythk/github-actions-new-app:latest
01d0da084e522431c85da7ecef67566ff602810221fe3f5f1bbbfc0693f06708


harry@NEW4090-G8:~/new-github-actions-practice$ docker ps
CONTAINER ID   IMAGE                                    COMMAND                CREATED              STATUS              PORTS                                         NAMES
01d0da084e52   harrythk/github-actions-new-app:latest   "bash entrypoint.sh"   About a minute ago   Up About a minute   0.0.0.0:8000->8000/tcp, [::]:8000->8000/tcp   zealous_hypatia




