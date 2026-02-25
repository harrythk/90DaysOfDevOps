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


























