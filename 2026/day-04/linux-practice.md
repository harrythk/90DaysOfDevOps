# Process commands

ps axu | grep ping
ubuntu      1457  0.0  0.2   8072  2712 pts/0    T    05:42   0:00 ping 8.8.8.8

pgrep ping
1457

ps -ef | grep nginx
ubuntu      1591    1074  0 06:11 pts/0    00:00:00 grep --color=auto nginx

# service commands
sudo apt install nginx -y

systemctl status nginx
nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: enabled)
     Active: active (running) since Wed 2026-01-28 06:19:07 UTC; 1min 36s ago

sudo systemctl stop nginx
systemctl status nginx
○ nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: enabled)
     Active: inactive (dead) since Wed 2026-01-28 06:23:03 UTC; 6s ago

sudo systemctl disable nginx
Synchronizing state of nginx.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
Executing: /usr/lib/systemd/systemd-sysv-install disable nginx
Removed "/etc/systemd/system/multi-user.target.wants/nginx.service".

# log commands
journalctl -u nginx
Jan 28 06:19:07 ip-172-31-18-78 systemd[1]: Starting nginx.service - A high performance web server and a reverse proxy server...
Jan 28 06:19:07 ip-172-31-18-78 systemd[1]: Started nginx.service - A high performance web server and a reverse proxy server.
Jan 28 06:23:03 ip-172-31-18-78 systemd[1]: Stopping nginx.service - A high performance web server and a reverse proxy server...
Jan 28 06:23:03 ip-172-31-18-78 systemd[1]: nginx.service: Deactivated successfully.
Jan 28 06:23:03 ip-172-31-18-78 systemd[1]: Stopped nginx.service - A high performance web server and a reverse proxy server.

tail -n 50 /var/log/syslog | grep CMD
2026-01-28T06:17:01.259934+00:00 ip-172-31-18-78 CRON[1709]: (root) CMD (cd / && run-parts --report /etc/cron.hourly)
2026-01-28T06:25:01.286133+00:00 ip-172-31-18-78 CRON[2420]: (root) CMD (test -x /usr/sbin/anacron || { cd / && run-parts --report /etc/cron.daily; })
2026-01-28T06:25:01.286490+00:00 ip-172-31-18-78 CRON[2421]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)

systemctl status ssh
ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: enabled)
    Drop-In: /usr/lib/systemd/system/ssh.service.d
             └─ec2-instance-connect.conf
     Active: active (running) since Wed 2026-01-28 05:17:08 UTC; 1h 17min ago

journalctl -u ssh

