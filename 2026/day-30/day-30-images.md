## Task 1: Docker Images

# Pull the nginx, ubuntu, and alpine images from Docker Hub
docker run -itd nginx
docker run -itd alpine
docker run -itd ubuntu

# List all images on your machine — note the sizes
MAGE                   ID             DISK USAGE   CONTENT SIZE   EXTRA
alpine:latest           25109184c71b       13.1MB         3.95MB    U   
flask-app-mini:latest   6d63c81c7973       88.2MB         21.4MB    U   
nginx:latest            341bf0f3ce6c        240MB         65.8MB    U   
ubuntu:latest           d1e2e92c075e        119MB         31.7MB    U  

# Compare ubuntu vs alpine — why is one much smaller?
Ubuntu is 119 PB in size while alpine is 13.1 MB in size. So, alpine is smaller in size.

# Inspect an image — what information can you see?
docker inspect d1e2e92c075e
It gives information about the environment path, OS name, version, size etc.

# Remove an image you no longer need
harry@NEW4090-G8:~/my-docker-project$ docker rmi 25109184c71b
Untagged: alpine:latest
Deleted: sha256:25109184c71bdad752c8312a8623239686a9a2071e8825f20acb8f2198c3f659

====================================================================================================================

# Task 2: Image Layers

# Run docker image history nginx — what do you see?
harry@NEW4090-G8:~/my-docker-project$ docker image history nginx
IMAGE          CREATED       CREATED BY                                      SIZE      COMMENT
341bf0f3ce6c   2 weeks ago   CMD ["nginx" "-g" "daemon off;"]                0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   STOPSIGNAL SIGQUIT                              0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   EXPOSE map[80/tcp:{}]                           0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   ENTRYPOINT ["/docker-entrypoint.sh"]            0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   COPY 30-tune-worker-processes.sh /docker-ent…   16.4kB    buildkit.dockerfile.v0
<missing>      2 weeks ago   COPY 20-envsubst-on-templates.sh /docker-ent…   12.3kB    buildkit.dockerfile.v0
<missing>      2 weeks ago   COPY 15-local-resolvers.envsh /docker-entryp…   12.3kB    buildkit.dockerfile.v0
<missing>      2 weeks ago   COPY 10-listen-on-ipv6-by-default.sh /docker…   12.3kB    buildkit.dockerfile.v0
<missing>      2 weeks ago   COPY docker-entrypoint.sh / # buildkit          8.19kB    buildkit.dockerfile.v0
<missing>      2 weeks ago   RUN /bin/sh -c set -x     && groupadd --syst…   86.6MB    buildkit.dockerfile.v0
<missing>      2 weeks ago   ENV DYNPKG_RELEASE=1~trixie                     0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   ENV PKG_RELEASE=1~trixie                        0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   ENV ACME_VERSION=0.3.1                          0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   ENV NJS_RELEASE=1~trixie                        0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   ENV NJS_VERSION=0.9.5                           0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   ENV NGINX_VERSION=1.29.5                        0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   LABEL maintainer=NGINX Docker Maintainers <d…   0B        buildkit.dockerfile.v0
<missing>      3 weeks ago   # debian.sh --arch 'amd64' out/ 'trixie' '@1…   87.4MB    debuerreotype 0.17

It gives history of a docker image i.e. how it was built in steps.

# Each line is a layer. Note how some layers show sizes and some show 0B
Some layer show 0B in size because they just contain metadata.

# Write in your notes: What are layers and why does Docker use them?
A layer in Docker is a read-only filesystem snapshot created for each instruction in a Dockerfile (FROM, RUN, COPY, ADD, etc.). If 10 containers use the same base image, Docker stores it only once.

====================================================================================================================

## Task 3: Container Lifecycle

# Practice the full lifecycle on one container:

# Create a container (without starting it)
harry@NEW4090-G8:~/my-docker-project$ docker create --name my-redis redis

harry@NEW4090-G8:~/my-docker-project$ docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                     PORTS                 NAMES
d00ee3af1a10   redis          "docker-entrypoint.s…"   28 seconds ago   Created                                          my-redis

# Start the container
harry@NEW4090-G8:~/my-docker-project$ docker start d00ee3af1a10

harry@NEW4090-G8:~/my-docker-project$ docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS                     PORTS                 NAMES
d00ee3af1a10   redis          "docker-entrypoint.s…"   About a minute ago   Up 4 seconds               6379/tcp              my-redis

# Pause it and check status
harry@NEW4090-G8:~/my-docker-project$ docker pause d00ee3af1a10

harry@NEW4090-G8:~/my-docker-project$ docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                       PORTS                 NAMES
d00ee3af1a10   redis          "docker-entrypoint.s…"   2 minutes ago    Up About a minute (Paused)   6379/tcp              my-redis

# Unpause it
harry@NEW4090-G8:~/my-docker-project$ docker unpause d00ee3af1a10

harry@NEW4090-G8:~/my-docker-project$ docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                     PORTS                 NAMES
d00ee3af1a10   redis          "docker-entrypoint.s…"   2 minutes ago    Up About a minute          6379/tcp              my-redis

# Stop it
harry@NEW4090-G8:~/my-docker-project$ docker stop d00ee3af1a10

CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                     PORTS                 NAMES
d00ee3af1a10   redis          "docker-entrypoint.s…"   3 minutes ago    Exited (0) 3 seconds ago                         my-redis

# Restart it
harry@NEW4090-G8:~/my-docker-project$ docker restart d00ee3af1a10

CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                      PORTS                 NAMES
d00ee3af1a10   redis          "docker-entrypoint.s…"   4 minutes ago    Up 2 seconds                6379/tcp              my-redis

# Kill it
harry@NEW4090-G8:~/my-docker-project$ docker kill d00ee3af1a10

CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                       PORTS                 NAMES
d00ee3af1a10   redis          "docker-entrypoint.s…"   4 minutes ago    Exited (137) 2 seconds ago                         my-redis

# Remove it
harry@NEW4090-G8:~/my-docker-project$ docker rm d00ee3af1a10

There is no entry of redis in docker ps -a.

====================================================================================================================

## Task 4: Working with Running Containers

# Run an Nginx container in detached mode
harry@NEW4090-G8:~/my-docker-project$ docker run -d nginx:latest

CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                      PORTS                 NAMES
76d6028a38a9   nginx:latest   "/docker-entrypoint.…"   5 seconds ago    Up 4 seconds                80/tcp                great_murdock

# View its logs
harry@NEW4090-G8:~/my-docker-project$ docker logs 76d6028a38a9
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2026/02/24 06:55:28 [notice] 1#1: using the "epoll" event method
2026/02/24 06:55:28 [notice] 1#1: nginx/1.29.5
2026/02/24 06:55:28 [notice] 1#1: built by gcc 14.2.0 (Debian 14.2.0-19) 
2026/02/24 06:55:28 [notice] 1#1: OS: Linux 6.6.87.2-microsoft-standard-WSL2
2026/02/24 06:55:28 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2026/02/24 06:55:28 [notice] 1#1: start worker processes
2026/02/24 06:55:28 [notice] 1#1: start worker process 30
2026/02/24 06:55:28 [notice] 1#1: start worker process 31
2026/02/24 06:55:28 [notice] 1#1: start worker process 32
2026/02/24 06:55:28 [notice] 1#1: start worker process 33
2026/02/24 06:55:28 [notice] 1#1: start worker process 34
2026/02/24 06:55:28 [notice] 1#1: start worker process 35
2026/02/24 06:55:28 [notice] 1#1: start worker process 36
2026/02/24 06:55:28 [notice] 1#1: start worker process 37

# View real-time logs (follow mode)
harry@NEW4090-G8:~/my-docker-project$ docker logs -f beec94b079ce

# Exec into the container and look around the filesystem
harry@NEW4090-G8:~/my-docker-project$ docker exec -it beec94b079ce bash

# Run a single command inside the container without entering it
harry@NEW4090-G8:~/my-docker-project$ docker exec stoic_tu ls
bin
boot
dev
docker-entrypoint.d
docker-entrypoint.sh
etc
home
lib
lib64
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var

# Inspect the container — find its IP address, port mappings, and mounts
harry@NEW4090-G8:~/my-docker-project$ docker inspect beec94b079ce

"IPAddress": "172.17.0.3",
"ExposedPorts": { "80/tcp": {}

No Mounts for NGINX.

====================================================================================================================

## Task 5: Cleanup

# Stop all running containers in one command
harry@NEW4090-G8:~/my-docker-project$ docker stop $(docker ps -q)
beec94b079ce
32ded1f426da
9ee93528efd0

CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                       PORTS     NAMES
beec94b079ce   nginx:latest   "/docker-entrypoint.…"   14 minutes ago   Exited (0) 6 seconds ago               stoic_tu
da8b6c503272   alpine         "/bin/sh"                38 minutes ago   Exited (0) 37 minutes ago              intelligent_proskuriakova
32ded1f426da   mysql:latest   "docker-entrypoint.s…"   24 hours ago     Exited (137) 5 seconds ago             mystifying_chatelet
9ee93528efd0   ubuntu         "/bin/bash"              26 hours ago     Exited (137) 5 seconds ago             flamboyant_spence

# Remove all stopped containers in one command
harry@NEW4090-G8:~/my-docker-project$ docker system prune 

harry@NEW4090-G8:~/my-docker-project$ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

# Remove unused images
harry@NEW4090-G8:~/my-docker-project$ docker image prune -a

harry@NEW4090-G8:~/my-docker-project$ docker images
IMAGE   ID             DISK USAGE   CONTENT SIZE   EXTRA

# Check how much disk space Docker is using
harry@NEW4090-G8:~/my-docker-project$ docker system df
TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          0         0         72.81MB   72.81MB (100%)
Containers      0         0         0B        0B
Local Volumes   2         0         436.7MB   436.7MB (100%)
Build Cache     46        0         94.16MB   94.16MB







