# Day 14 Practice

## OSI layers (L1–L7) vs TCP/IP stack
- OSI model is more of a conceptual model made up of 7 layers whereas TCP/IP model is used in real world and it is of 4 layers (Application, Transport, Internet, Network Access).
- TCP/IP merges OSI layers (L5–L7 → Application, L1–L2 → Network Access), keeping Transport (L4) and Network/Internet (L3) separate.

## Where IP, TCP/UDP, HTTP/HTTPS, DNS sit in the stack
IP is on Internet layer, TCP/UDP is on Transport layer, HTTP / HTTPS is on Application layer, DNS is on Application layer.

## One real example: “curl https://example.com = App layer over TCP over IP”
curl https://google.com
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="https://www.google.com/">here</A>.
</BODY></HTML>

## Hands-on Checklist

# hostname -I
Gives the 2 IP address used by my EC2 instance.

# ping 8.8.8.8
64 bytes from 8.8.8.8: icmp_seq=1 ttl=117 time=0.662 ms
Latency: 0.662 ms 
Packet loss: 0% 

# traceroute 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  240.4.244.43 (240.4.244.43)  1.248 ms 240.4.244.40 (240.4.244.40)  1.380 ms  1.946 ms
 2  242.13.251.133 (242.13.251.133)  1.496 ms 242.13.251.1 (242.13.251.1)  1.534 ms *
 3  * * *
 4  * * 99.82.176.25 (99.82.176.25)  0.712 ms
 5  * * *
 6  dns.google (8.8.8.8)  0.609 ms  0.615 ms  0.621 ms

Low latency on each hop and no response on hop 3 and 5. 

# ss -tulpn
tcp           LISTEN         0              511                                 [::]:80                            [::]:*             users:(("nginx",pid=592,fd=6),("nginx",pid=591,fd=6),("nginx",pid=580,fd=6))

# dig google.com
google.com.             247     IN      A       209.85.202.101
google.com.             247     IN      A       209.85.202.139
google.com.             247     IN      A       209.85.202.100
google.com.             247     IN      A       209.85.202.138
google.com.             247     IN      A       209.85.202.102
google.com.             247     IN      A       209.85.202.113

# curl -I https://www.google.com
HTTP/2 200 
200 means successful.

# netstat -an | head
5 ports are in LISTEN state while 1 is showing ESTABLISHED

## Mini Task: Port Probe & Interpret

# sudo ss -tulpn
tcp           LISTEN         0              4096                                [::]:22                            [::]:*             users:(("sshd",pid=1180,fd=4),("systemd",pid=1,fd=91))

# sudo nc -zv localhost 22
Connection to localhost (127.0.0.1) 22 port [tcp/ssh] succeeded!

# Write one line: is it reachable? If not, what’s the next check? (e.g., service status, firewall).
It is reachable on port 22 that is why I am able to connect to the ec2 instance. If some port shows not reachable for a service that the service status needs to be checked first using systemctl status <service>.


# Which command gives you the fastest signal when something is broken?
Systemctl status <service> - it shows if some service is failed. After that journalctl can be used.

# What layer (OSI/TCP-IP) would you inspect next if DNS fails? If HTTP 500 shows up?
If DNS fails, we need to check on Application layer. HTTP 500 will show application layer problem, it shows internal server error.

# Two follow-up checks you’d run in a real incident.
We will use dig and journalctl in case of real incident.


