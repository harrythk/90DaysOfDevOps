

## Processes & services:

ps aux | grep nginx 
root         602  0.0  0.1  11160  1732 ?        Ss   05:01   0:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
www-data     604  0.0  0.4  12884  4556 ?        S    05:01   0:00 nginx: worker process
www-data     605  0.0  0.4  12884  4496 ?        S    05:01   0:00 nginx: worker process
ubuntu      1603  0.0  0.2   7076  2232 pts/2    S+   05:31   0:00 grep --color=auto nginx

Shows the cpu / memory utilization at the poing when the command is run. Also shows the process ID of the service, in this case it is 602.

systemctl status nginx
nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: enabled)
     Active: active (running) since Thu 2026-02-05 05:01:09 UTC; 40min ago
       Docs: man:nginx(8)
    Process: 548 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
    Process: 567 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
   Main PID: 602 (nginx)
      Tasks: 3 (limit: 1017)
     Memory: 3.7M (peak: 3.9M)
        CPU: 34ms
     CGroup: /system.slice/nginx.service
             ├─602 "nginx: master process /usr/sbin/nginx -g daemon on; master_process on;"
             ├─604 "nginx: worker process"
             └─605 "nginx: worker process"
shows status of service (nginx in this case) along with process ID.

journalctl -u nginx
shows logs of the service along with date and time.

## File skills
echo "Day 12 practice" >> Day12.txt
mkdir Day12
cp Day12.txt Day12

ls -l Day12
total 4
-rw-rw-r-- 1 ubuntu ubuntu 16 Feb  5 06:02 Day12.txt

## 5 commands in case of an incident
ps aux
top
systemctl status <service>
ls -l
journalctl -u <service> -n 50

## 1.Which 3 commands save you the most time right now, and why?
ls -l ---- shows all the files and folers in the directory
systemctl status <service> --- shows the status of a service
ps aux | grep <service> 

## 2.How do you check if a service is healthy? List the exact 2–3 commands you’d run first.
systemctl status <service> ---- systemd’s view of status of service
journalctl -u <service> -n 50 ---- shows any problem with service in logs
ss -lntp ------ ports listening 

## 3.How do you safely change ownership and permissions without breaking access? Give one example command.
sudo chmod 750 file/directory ---- change permission of a file/directory
sudo chown owner:group file/directory ----- change owner / group of a file/directory

## 4.What will you focus on improving in the next 3 days?
I am working on Python (mostly on atomation part and API), Systemd process and shell scripts.







