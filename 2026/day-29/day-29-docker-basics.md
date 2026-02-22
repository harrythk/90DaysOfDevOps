## Task 1: What is Docker?

# What is a container and why do we need them?
Containers are a solution to the problem of how to get software to run reliably when moved from one computing environment to another. 
We need continers to make sure that applications run in any system without thinking about required software and variables.

# Containers vs Virtual Machines — what's the real difference?
Virtual Machines (VMs) run a full OS on top of a hypervisor — each VM has its own kernel, so they’re heavier and use more RAM/CPU (e.g., on Amazon EC2).
Containers share the host OS kernel and package only the app + dependencies — they’re lightweight, start faster, and are managed by tools like Docker.

# What is the Docker architecture? (daemon, client, images, containers, registry)
Daemon - : The background process running on the host machine that performs most of task.
Client: The primary command-line interface with which users interact with Docker.
Containers: Keeps application and its dependencies.
images: blueprints used to create Docker containers.
Registry: A centralized storage and distribution system for Docker images.

==================================================================================================================================================================

## Task 2: Install Docker

# Install Docker on your machine (or use a cloud instance)
# Verify the installation

docker --version
Docker version 29.2.1, build a5c7197

# Run the hello-world container
# Read the output carefully — it explains what just happened

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

==================================================================================================================================================================

## Task 3: Run Real Containers

# Run an Nginx container and access it in your browser
docker run -d -p 80:80 --name my-nginx nginx

# Run an Ubuntu container in interactive mode — explore it like a mini Linux machine
docker run -itd ubuntu
docker exec -it 6715dcb00dd9 bash

# List all running containers
ubuntu@ip-172-31-47-89:~/docker-projects$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS                                 NAMES
6715dcb00dd9   ubuntu    "/bin/bash"              30 seconds ago       Up 29 seconds                                             reverent_cartwright
94e22fac6b24   nginx     "/docker-entrypoint.…"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, [::]:80->80/tcp   my-nginx

# List all containers (including stopped ones)
ubuntu@ip-172-31-47-89:~/docker-projects$ docker ps -a
CONTAINER ID   IMAGE         COMMAND                  CREATED          STATUS                      PORTS                                 NAMES
6715dcb00dd9   ubuntu        "/bin/bash"              2 minutes ago    Up 2 minutes                                                      reverent_cartwright
94e22fac6b24   nginx         "/docker-entrypoint.…"   3 minutes ago    Up 3 minutes                0.0.0.0:80->80/tcp, [::]:80->80/tcp   my-nginx
3050675ca838   hello-world   "/hello"                 12 minutes ago   Exited (0) 12 minutes ago                                         zen_chandrasekhar

# Stop and remove a container
ubuntu@ip-172-31-47-89:~/docker-projects$ docker stop 94e22fac6b24 && docker rm 94e22fac6b24
94e22fac6b24
94e22fac6b24

==================================================================================================================================================================

## Task 4: Explore

# Run a container in detached mode — what's different?
If you run a container in detached mode (-d) you dont see its logs and it runs in the background. It keeps on running event if terminal is closed.

# Give a container a custom name
# Map a port from the container to your host

docker run -d -p 80:80 --name my-nginx nginx

# Check logs of a running container
ubuntu@ip-172-31-47-89:~/docker-projects$ docker logs 31e8275716e2
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2026/02/22 15:37:46 [notice] 1#1: using the "epoll" event method
2026/02/22 15:37:46 [notice] 1#1: nginx/1.29.5
2026/02/22 15:37:46 [notice] 1#1: built by gcc 14.2.0 (Debian 14.2.0-19)
2026/02/22 15:37:46 [notice] 1#1: OS: Linux 6.17.0-1007-aws
2026/02/22 15:37:46 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2026/02/22 15:37:46 [notice] 1#1: start worker processes
2026/02/22 15:37:46 [notice] 1#1: start worker process 30
2026/02/22 15:37:46 [notice] 1#1: start worker process 31

# Run a command inside a running container
root@31e8275716e2:/# ls -a
.   .dockerenv  boot  docker-entrypoint.d   etc   lib    media  opt   root  sbin  sys  usr
..  bin         dev   docker-entrypoint.sh  home  lib64  mnt    proc  run   srv   tmp  var







 
