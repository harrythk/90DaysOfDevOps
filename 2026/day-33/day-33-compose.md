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

Write a docker-compose.yml that runs:
A WordPress container
A MySQL container
They should:

Be on the same network (Compose does this automatically)
MySQL should have a named volume for data persistence
WordPress should connect to MySQL using the service name
Start it, access WordPress in your browser, and set it up.


services:
  mysql:
    image: mysql:8.0
    container_name: mysql-wordpress
    environment:
      MYSQL_USER: wpuser
      MYSQL_ROOT_PASSWORD: Test@123
      MYSQL_DATABASE: wordpressdb
      MYSQL_PASSWORD: wppass
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost", "-u", "root", "-pTest@123"]
      interval: 10s
      timeout: 5s
      retries: 3
      start_period: 30s
    ports:
      - "3306:3306"
    volumes:
      - wordpress_sql:/var/lib/mysql 
    networks:
      - wordpress-nw

  wordpress:
    image: wordpress
    container_name: cont_wordpress
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: mysql
      WORDPRESS_DB_NAME: wordpressdb
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppass
    networks:
      - wordpress-nw
    depends_on:
      mysql:
        condition: service_healthy

networks:
  wordpress-nw:
    driver: bridge
volumes:
  wordpress_sql:


Verify: Stop and restart with docker compose down and docker compose up — is your WordPress data still there? - Yes the data is still there.

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++










