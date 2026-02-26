## Task 1: Your First Dockerfile

# Create a folder called my-first-image
# Inside it, create a Dockerfile that:
  Uses ubuntu as the base image
  Installs curl
  Sets a default command to print "Hello from my custom image!"

Dockerfile:
FROM ubuntu:22.04

WORKDIR /app

RUN apt update
RUN apt install -y curl

CMD ["echo","Hello from my custom image!"]

# Build the image and tag it my-ubuntu:v1

harry@NEW4090-G8:~/my-docker-project/my-first-image$ docker build -t my-ubuntu:v1 .

harry@NEW4090-G8:~/my-docker-project/my-first-image$ docker images
IMAGE          ID             DISK USAGE   CONTENT SIZE   EXTRA
my-ubuntu:v1   f295a45a3342        252MB         82.3MB 

# Run a container from your image

harry@NEW4090-G8:~/my-docker-project/my-first-image$ docker run -it my-ubuntu:v1
Hello from my custom image!

=============================================================================================================================================================

## Task 2: Dockerfile Instructions

# Create a new Dockerfile that uses all of these instructions:
  FROM — base image
  RUN — execute commands during build
  COPY — copy files from host to image
  WORKDIR — set working directory
  EXPOSE — document the port
  CMD — default command
  Build and run it. Understand what each line does.

harry@NEW4090-G8:~/my-docker-project/my-http-server/simple-http-server$ vim Dockerfile

FROM alpine:latest

WORKDIR /app

COPY . .

EXPOSE 8000

RUN apk --no-cache -U add python3 && \
    apk upgrade --no-cache -U -a

CMD ["python3", "-m", "http.server", "8000"]

=============================================================================================================================================================

## Task 3: CMD vs ENTRYPOINT

# Create an image with CMD ["echo", "hello"] — run it, then run it with a custom command. What happens?

harry@NEW4090-G8:~/my-docker-project/my-http-server/cmd-test$ vim Dockerfile
FROM alpine:latest

CMD ["echo", "hello"]

harry@NEW4090-G8:~/my-docker-project/my-http-server/cmd-test$ docker run test-cmd:latest echo Hello world
Hello world

# Create an image with ENTRYPOINT ["echo"] — run it, then run it with additional arguments. What happens?

FROM alpine:latest

ENTRYPOINT ["echo"]

harry@NEW4090-G8:~/my-docker-project/Entrypoint-test$ docker run entrypoint-test:latest Hello India
Hello India

# Write in your notes: When would you use CMD vs ENTRYPOINT?

CMD provides a default command that can be overwritten during execusion.
ENTRYPOINT takes arguments as paramter to run.

=============================================================================================================================================================

## Task 4: Build a Simple Web App Image

# Create a small static HTML file (index.html) with any content

<!DOCTYPE html>
<html>
<head>
    <title>My Docker Page</title>
</head>
<body>
    <h1>Hello from my container 🚀</h1>
    <p>This is my HTML file.</p>
</body>
</html>

# Write a Dockerfile that:
Uses nginx:alpine as base
Copies your index.html to the Nginx web directory

FROM nginx:alpine
COPY index.html /usr/share/nginx/html/
EXPOSE 80

# Build and tag it my-website:v1
docker build -t my-website:v1 .

# Run it with port mapping and access it in your browser
harry@NEW4090-G8:~/my-docker-project/simple_webapp_image$ docker run -d -p 80:80 my-website:v1
356cdc168212f274399306b3dbc989554e382eca2bd5677d1dd6f7fd0523a812
<img width="257" height="96" alt="image" src="https://github.com/user-attachments/assets/3200e964-582b-4420-a7b1-e4e48ba15743" />

=============================================================================================================================================================



















