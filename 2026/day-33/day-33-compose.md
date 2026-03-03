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

## Task 4: Compose Commands
Practice and document these:

# Start services in detached mode
harry@NEW4090-G8:~/my-docker-project/two-container-setup$ docker compose up -d
[+] up 3/3
 ✔ Network two-container-setup_wordpress-nw Created                                                                   0.1s
 ✔ Container mysql-wordpress                Healthy                                                                   7.0s
 ✔ Container cont_wordpress                 Created                                                                   0.3s

# View running services
harry@NEW4090-G8:~/my-docker-project/two-container-setup$ docker compose ps
NAME              IMAGE       COMMAND                  SERVICE     CREATED              STATUS                        PORTS
cont_wordpress    wordpress   "docker-entrypoint.s…"   wordpress   About a minute ago   Up About a minute             0.0.0.0:8080->80/tcp, [::]:8080->80/tcp
mysql-wordpress   mysql:8.0   "docker-entrypoint.s…"   mysql       About a minute ago   Up About a minute (healthy)   0.0.0.0:3306->3306/tcp, [::]:3306->3306/tcp

# View logs of all services
harry@NEW4090-G8:~/my-docker-project/two-container-setup$ docker compose logs -f
mysql-wordpress  | 2026-03-03 12:19:15+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.0.45-1.el9 started.
mysql-wordpress  | 2026-03-03 12:19:15+00:00 [Note] [Entrypoint]: Switching to dedicated user 'mysql'
mysql-wordpress  | 2026-03-03 12:19:15+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.0.45-1.el9 started.
mysql-wordpress  | '/var/lib/mysql/mysql.sock' -> '/var/run/mysqld/mysqld.sock'
mysql-wordpress  | 2026-03-03T12:19:15.919258Z 0 [Warning] [MY-011068] [Server] The syntax '--skip-host-cache' is deprecated and will be removed in a future release. Please use SET GLOBAL host_cache_size=0 instead.
mysql-wordpress  | 2026-03-03T12:19:15.922686Z 0 [System] [MY-010116] [Server] /usr/sbin/mysqld (mysqld 8.0.45) starting as process 1
mysql-wordpress  | 2026-03-03T12:19:15.939948Z 1 [System] [MY-013576] [InnoDB] InnoDB initialization has started.
mysql-wordpress  | 2026-03-03T12:19:16.525130Z 1 [System] [MY-013577] [InnoDB] InnoDB initialization has ended.
mysql-wordpress  | 2026-03-03T12:19:16.720092Z 0 [System] [MY-010229] [Server] Starting XA crash recovery...
mysql-wordpress  | 2026-03-03T12:19:16.736539Z 0 [System] [MY-010232] [Server] XA crash recovery finished.
mysql-wordpress  | 2026-03-03T12:19:16.841861Z 0 [Warning] [MY-010068] [Server] CA certificate ca.pem is self signed.
mysql-wordpress  | 2026-03-03T12:19:16.841916Z 0 [System] [MY-013602] [Server] Channel mysql_main configured to support TLS. Encrypted connections are now supported for this channel.
mysql-wordpress  | 2026-03-03T12:19:16.846863Z 0 [Warning] [MY-011810] [Server] Insecure configuration for --pid-file: Location '/var/run/mysqld' in the path is accessible to all OS users. Consider choosing a different directory.
mysql-wordpress  | 2026-03-03T12:19:16.871396Z 0 [System] [MY-011323] [Server] X Plugin ready for connections. Bind-address: '::' port: 33060, socket: /var/run/mysqld/mysqlx.sock
mysql-wordpress  | 2026-03-03T12:19:16.871585Z 0 [System] [MY-010931] [Server] /usr/sbin/mysqld: ready for connections. Version: '8.0.45'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server - GPL.
cont_wordpress   | WordPress not found in /var/www/html - copying now...
cont_wordpress   | Complete! WordPress has been successfully copied to /var/www/html
cont_wordpress   | No 'wp-config.php' found in /var/www/html, but 'WORDPRESS_...' variables supplied; copying 'wp-config-docker.php' (WORDPRESS_DB_HOST WORDPRESS_DB_NAME WORDPRESS_DB_PASSWORD WORDPRESS_DB_USER)
cont_wordpress   | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.18.0.3. Set the 'ServerName' directive globally to suppress this message
cont_wordpress   | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.18.0.3. Set the 'ServerName' directive globally to suppress this message
cont_wordpress   | [Tue Mar 03 12:19:22.403014 2026] [mpm_prefork:notice] [pid 1:tid 1] AH00163: Apache/2.4.66 (Debian) PHP/8.3.30 configured -- resuming normal operations
cont_wordpress   | [Tue Mar 03 12:19:22.403061 2026] [core:notice] [pid 1:tid 1] AH00094: Command line: 'apache2 -D FOREGROUND'

# View logs of a specific service
harry@NEW4090-G8:~/my-docker-project/two-container-setup$ docker compose logs wordpress
cont_wordpress  | WordPress not found in /var/www/html - copying now...
cont_wordpress  | Complete! WordPress has been successfully copied to /var/www/html
cont_wordpress  | No 'wp-config.php' found in /var/www/html, but 'WORDPRESS_...' variables supplied; copying 'wp-config-docker.php' (WORDPRESS_DB_HOST WORDPRESS_DB_NAME WORDPRESS_DB_PASSWORD WORDPRESS_DB_USER)
cont_wordpress  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.18.0.3. Set the 'ServerName' directive globally to suppress this message
cont_wordpress  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.18.0.3. Set the 'ServerName' directive globally to suppress this message
cont_wordpress  | [Tue Mar 03 12:19:22.403014 2026] [mpm_prefork:notice] [pid 1:tid 1] AH00163: Apache/2.4.66 (Debian) PHP/8.3.30 configured -- resuming normal operations
cont_wordpress  | [Tue Mar 03 12:19:22.403061 2026] [core:notice] [pid 1:tid 1] AH00094: Command line: 'apache2 -D FOREGROUND'

# Stop services without removing
harry@NEW4090-G8:~/my-docker-project/two-container-setup$ docker compose stop
[+] stop 2/2
 ✔ Container cont_wordpress  Stopped                                                                                                                           1.3s
 ✔ Container mysql-wordpress Stopped

# Remove everything (containers, networks)
harry@NEW4090-G8:~/my-docker-project/two-container-setup$ docker compose down
[+] down 3/3
 ✔ Container cont_wordpress                 Removed                                                                                                            0.0s
 ✔ Container mysql-wordpress                Removed                                                                                                            0.1s
 ✔ Network two-container-setup_wordpress-nw Removed                                                                                                            0.3s

# Rebuild images if you make a change
harry@NEW4090-G8:~/my-docker-project/two-container-setup$ docker compose up -d --build
[+] up 3/3
 ✔ Network two-container-setup_wordpress-nw Created                                                                                                            0.1s
 ✔ Container mysql-wordpress                Healthy                                                                                                            6.3s
 ✔ Container cont_wordpress                 Created                                                                                                            0.2s

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 5: Environment Variables

# Add environment variables directly in your docker-compose.yml

services:
  mysql:
    image: mysql:8.0
    container_name: mysql-wordpress
    environment:
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
  wordpress:
    image: wordpress
    container_name: cont_wordpress
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: mysql
      WORDPRESS_DB_NAME: ${MYSQL_DATABASE}
      WORDPRESS_DB_USER: ${MYSQL_USER}
      WORDPRESS_DB_PASSWORD: ${MYSQL_PASSWORD}

# Create a .env file and reference variables from it in your compose file
MYSQL_USER: wpuser
MYSQL_ROOT_PASSWORD: Test@123
MYSQL_DATABASE: wordpressdb
MYSQL_PASSWORD: wppass

# Verify the variables are being picked up
harry@NEW4090-G8:~/my-docker-project/two-container-setup$ docker exec -it mysql-wordpress env
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=f5beff814c19
TERM=xterm
MYSQL_USER=wpuser
MYSQL_ROOT_PASSWORD=Test@123
MYSQL_DATABASE=wordpressdb
MYSQL_PASSWORD=wppass
GOSU_VERSION=1.19
MYSQL_MAJOR=8.0
MYSQL_VERSION=8.0.45-1.el9
MYSQL_SHELL_VERSION=8.0.45-1.el9
HOME=/root













