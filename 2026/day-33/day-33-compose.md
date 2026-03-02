## Task 1: Install & Verify

# Check if Docker Compose is available on your machine

harry@NEW4090-G8:~/my-docker-project$ docker compose version 
Docker Compose version v5.0.2

# Verify the version
The version is 5.0.2

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 2: Your First Compose File

# Create a folder compose-basics
harry@NEW4090-G8:~/my-docker-project$ mkdir compose-basics

# Write a docker-compose.yml that runs a single Nginx container with port mapping

services:
  nginx:
    image: nginx:latest
    container_name: mynginx
    ports:
      - "8080:80"

# Start it with docker compose up
harry@NEW4090-G8:~/my-docker-project/compose-basics$ docker compose up
Attaching to mynginx

# Access it in your browser
<img width="1102" height="281" alt="image" src="https://github.com/user-attachments/assets/4a1b6d6a-fec7-4166-a59e-636673b30f70" />

# Stop it with docker compose down
harry@NEW4090-G8:~/my-docker-project/compose-basics$ docker compose down
[+] down 2/2
 ✔ Container mynginx              Removed                                                                                                                      0.4s
 ✔ Network compose-basics_default Removed 

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 3: Two-Container Setup














