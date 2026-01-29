uname -a
Linux ip-172-31-18-78 6.14.0-1018-aws #18~24.04.1-Ubuntu SMP Mon Nov 24 19:46:27 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux
# gives information about the IP address, kernel version, release date, architecture etc.


cat /etc/os-release
PRETTY_NAME="Ubuntu 24.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.3 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=noble
LOGO=ubuntu-logo
# gives information about OS, version detail etc.

top / htop
# shows live running process

ps -o pid,pcpu,pmem,comm -p 536
    PID %CPU %MEM COMMAND
    536  0.0  0.3 cron
# shows CPU, memory usage by the particular process / PID


free -h
               total        used        free      shared  buff/cache   available
Mem:           914Mi       366Mi       268Mi       2.7Mi       437Mi       547Mi
Swap:             0B          0B          0B
# shows total memory, used and free memory


df -h
Filesystem       Size  Used Avail Use% Mounted on
/dev/root        6.8G  2.3G  4.5G  34% /
tmpfs            458M     0  458M   0% /dev/shm
tmpfs            183M  872K  182M   1% /run
tmpfs            5.0M     0  5.0M   0% /run/lock
efivarfs         128K  3.8K  120K   4% /sys/firmware/efi/efivars
/dev/nvme0n1p16  881M   89M  730M  11% /boot
/dev/nvme0n1p15  105M  6.2M   99M   6% /boot/efi
tmpfs             92M   12K   92M   1% /run/user/1000
# shows file system and the disk space usage


sudo du -sh /var/log
45M     /var/log
# shows disk space used by /var/log folder

ss -tulpn
Netid       State        Recv-Q       Send-Q                  Local Address:Port               Peer Address:Port       Process
udp         UNCONN       0            0                           127.0.0.1:323                     0.0.0.0:*
udp         UNCONN       0            0                          127.0.0.54:53                      0.0.0.0:*
udp         UNCONN       0            0                       127.0.0.53%lo:53                      0.0.0.0:*
udp         UNCONN       0            0                   172.31.18.78%ens5:68                      0.0.0.0:*
udp         UNCONN       0            0                               [::1]:323                        [::]:*
tcp         LISTEN       0            4096                          0.0.0.0:22                      0.0.0.0:*
tcp         LISTEN       0            4096                       127.0.0.54:53                      0.0.0.0:*
tcp         LISTEN       0            4096                    127.0.0.53%lo:53                      0.0.0.0:*
tcp         LISTEN       0            4096                             [::]:22                         [::]:*
# shows which port are currently listening along with process.

curl -I http://localhost
HTTP/1.1 200 OK
Server: nginx/1.24.0 (Ubuntu)
Date: Thu, 29 Jan 2026 06:53:16 GMT
Content-Type: text/html
Content-Length: 615
Last-Modified: Wed, 28 Jan 2026 06:19:06 GMT
Connection: keep-alive
ETag: "6979aa5a-267"
Accept-Ranges: bytes
# shows which service is running on the port
