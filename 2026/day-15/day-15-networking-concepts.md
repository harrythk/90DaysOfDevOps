## Task 1: DNS – How Names Become IPs

# Explain in 3–4 lines: what happens when you type google.com in a browser?
- When we type google.com in browser, the system reaches out to DNS server to get the FQDN resolved. Then DNS server provides the IP address of the google servers. After that the system sends a HTTP/HTTPS request to the google servers ip address and gets the response.


# What are these record types? Write one line each:

A - Maps a domain name to an IPv4 address.
AAA - Maps a domain name to an IPv6 address.
CNAME - Aliases one domain name to another domain name.
MX - Specifies the mail servers responsible for receiving email for a domain.
NS - Defines the authoritative name servers for a domain.


# Run: dig google.com — identify the A record and TTL from the output

A record - 209.85.202.138, 209.85.202.139, 209.85.202.113, 209.85.202.100, 209.85.202.101, 209.85.202.102
TTL - 254 ms

## Task 2: IP Addressing

# What is an IPv4 address? How is it structured? (e.g., 192.168.1.10)
- The IP address is of 32 bits. It has 4 octets, separated by dots.

# Difference between public and private IPs — give one example of each
- Public IP address is accessible globally and Private IP address is used inside a local network.
- Public IP example is 8.8.8.8
- Private Ip example is 172.16.x.x

# What are the private IP ranges?
10.0.0.0 – 10.255.255.255 
172.16.0.0 – 172.31.255.255 
192.168.0.0 – 192.168.255.255 

# Run: ip addr show — identify which of your IPs are private
 My prvate IP address is 172.31.18.78 and 172.17.0.1


 ## Task 3: CIDR & Subnetting

# What does /24 mean in 192.168.1.0/24?
It means that 24 bits are alreday used and 8 bits are availabe. So, the subnet mask is 255.255.255.0 and IP address range available is 192.168.1.1 – 192.168.1.254.

# How many usable hosts in a /24? A /16? A /28?
/24 = 254 usable hosts
/16  = 65,534 usable hosts
/28 = 14 usable hosts

# Explain in your own words: why do we subnet?
It helps use ip address efiiciently and we don't need too many public ip address.

# Quick exercise — fill in:
CIDR	Subnet Mask	  Total IPs	Usable Hosts
/24	  255.255.255.0  256      254
/16	  255.255.0.0    65536    65234
/28	  255.255.255.240 16      14


## Task 4: Ports – The Doors to Services

# What is a port? Why do we need them?
A port identifies a specific service on a machine. The service accepts packets coming on that specific port.

# Document these common ports:
22 - SSH
80 - HTTP
442 - HTTPS
53 - DNS
33036 - MySQL
6379 - Redis
27017 - MongoDB

# Run ss -tulpn — match at least 2 listening ports to their services
port 22 is being used by sshd and port 80 is used by nginx
tcp           LISTEN         0              511                                 [::]:80                            [::]:*             users:(("nginx",pid=591,fd=6),("nginx",pid=590,fd=6),("nginx",pid=587,fd=6))
tcp           LISTEN         0              4096                                [::]:22                            [::]:*             users:(("sshd",pid=1171,fd=4),("systemd",pid=1,fd=91))


## Task 5: Putting It Together

# You run curl http://myapp.com:8080 — what networking concepts from today are involved?
It has DNS resolution - Resolves myapp.com to an IP address.
Port: 8080 tells which service to connect to.
TCP: Establishes a reliable connection to the server.
HTTP: sends an HTTP request

# Your app can't reach a database at 10.0.1.50:3306 — what would you check first?
I will see if the server ip address is reachable with ping. Then I will see if MySQL is listening on port 3306. I will also check if port 3306 is allowed on firewall with telnet.





