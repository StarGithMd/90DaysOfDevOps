Linux process management ensures smooth multitasking, resource optimization, and system stability.:

Linux servers usually handle processes in different states depending on resource availability. There are the main process states in Linux.
- Process States:
- Running – actively executing
- Sleeping – waiting for resources/events
- Stopped – paused by a signal
- Zombie – terminated but not cleaned up

top - Display Linux processes

- The top program provides a dynamic real-time view of a running Linux system.

ps - Displays information about active processes and report a snapshot of the current processes.
# top
top - 01:43:45 up 12 min,  1 user,  load average: 0.01, 0.00, 0.00
Tasks:  28 total,   1 running,  27 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.3 sy,  0.0 ni, 99.7 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   7636.2 total,   7173.4 free,    471.0 used,    140.1 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   7165.2 avail Mem
--------------------------------------------------------------------------------
    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
      1 root      20   0    0.0p   0.0p   0.0p S   0.0   0.2   0:00.61 systemd
      2 root      20   0    0.0p   0.0p   0.0p S   0.0   0.0   0:00.00 init-systemd(Ub
      7 root      20   0    0.0p   0.0p   0.0p S   0.0   0.0   0:00.00 init
     53 root      19  -1    0.0p   0.0p   0.0p S   0.0   0.2   0:00.16 systemd-journal
 
# ps -e
PID TTY          TIME CMD
      1 ?        00:00:00 systemd
      2 ?        00:00:00 init-systemd(Ub
      7 ?        00:00:00 init
     53 ?        00:00:00 systemd-journal

# ps -ef |grep 53
root          53       1  0 01:31 ?        00:00:00 /usr/lib/systemd/systemd-journald
root         560     295  0 01:51 pts/0    00:00:00 grep --color=auto 53

These are the important monitoring commands used in Linux.
- ps 		: Lists processes and thier IDs.
- top		: Monitor disk I/O usage.
- vmstat	: System performance (CPU, memory, I/O).
- systemctl	: Manage services under systemd.
- journalctl: View logs for troubleshooting.

- kill		: Use carefully—verify PID before terminating.
- pkill, killall: Prefer for convenience, but confirm process names.
- kill -9	: Avoid, unless necessary (it bypasses cleanup).
- nice 		: Adjust priorities with nice to prevent resource hogging.
- top/htop	: Monitor regularly to detect issues early.
- jobs		: Show background jobs
- systemctl status service-name : See the service running status before startting troubleshooting.

Networking commands (ping, ip addr, dig, curl, etc.)
- ping (Packet Internet Groper)	: Send ICMP ECHO_REQUEST to network hosts, Generally used for Check Connectivity & verifies reachability a host & domain.

Example:
# ping google.com
PING google.com (172.217.26.46) 56(84) bytes of data.
64 bytes from tzdelb-ap-in-f14.1e100.net (172.217.26.46): icmp_seq=1 ttl=117 time=12.9 ms
64 bytes from tzdelb-ap-in-f14.1e100.net (172.217.26.46): icmp_seq=2 ttl=117 time=13.3 ms
64 bytes from tzdelb-ap-in-f14.1e100.net (172.217.26.46): icmp_seq=3 ttl=117 time=8.79 ms

# ping -c 2 google.com		>> Sends 2 packets and shows the round-trip time
PING google.com (172.217.26.46) 56(84) bytes of data.
64 bytes from tzdelb-ap-in-f14.1e100.net (172.217.26.46): icmp_seq=1 ttl=117 time=10.4 ms
64 bytes from tzdelb-ap-in-f14.1e100.net (172.217.26.46): icmp_seq=2 ttl=117 time=11.2 ms

# ping -i 3 google.com	>> Sends a ping every 3 seconds to monitoring network stability over time
PING google.com (172.217.26.46) 56(84) bytes of data.
64 bytes from tzdelb-ap-in-f14.1e100.net (172.217.26.46): icmp_seq=1 ttl=117 time=10.8 ms
64 bytes from tzdelb-ap-in-f14.1e100.net (172.217.26.46): icmp_seq=2 ttl=117 time=34.8 ms
64 bytes from tzdelb-ap-in-f14.1e100.net (172.217.26.46): icmp_seq=3 ttl=117 time=7.64 ms

# ping -f google.com	>> Sends packets as fast as possible to check stress-tests & network performance.
PING google.com (172.217.26.46) 56(84) bytes of data.
...............................................................................................
--- google.com ping statistics ---
20229 packets transmitted, 20091 received, 0.682189% packet loss, time 174850ms
rtt min/avg/max/mdev = 3.814/8.359/56.506/2.292 ms, pipe 4, ipg/ewma 8.643/7.502 ms

# ip addr | ip a | ifconfig			>> Lists every network interface, their IP addresses, MAC addresses, and current state (wired, wireless, loopback, virtual)
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet 10.255.255.254/32 brd 10.255.255.254 scope global lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:15:5d:bc:28:52 brd ff:ff:ff:ff:ff:ff
    inet 172.19.101.31/20 brd 172.19.111.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::215:5dff:febc:2852/64 scope link
       valid_lft forever preferred_lft forever

# ip addr |grep eth0
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    inet 172.19.101.31/20 brd 172.19.111.255 scope global eth0

# # hostname -a			>> Display hostname
DESKTOP-CPK0PUB

# # hostname -I			>> Display hostn ip address
172.19.101.31

# traceroute google.com	>> Displays all intermediate routers between your system and Google
Command 'traceroute' not found, but can be installed with:
apt install inetutils-traceroute  # version 2:2.5-3ubuntu4.1, or
apt install traceroute            # version 1:2.1.5-1 			

# traceroute -I google.com	>> Uses ICMP instead of UDP packets when default traceroute is blocked or filtered
traceroute to google.com (172.217.26.46), 30 hops max, 60 byte packets
 1  DESKTOP-CPK0PUB.mshome.net (172.19.96.1)  0.676 ms  5.141 ms *
 2  192.168.1.1 (192.168.1.1)  1.959 ms  2.330 ms *
 3  10.105.61.1 (10.105.61.1)  14.372 ms  14.334 ms *
 4  43.231.58.5 (43.231.58.5)  14.144 ms * *
 5  * * *
 6  * * *
 7  * * *
 8  * * *
 9  tzdelb-ap-in-f14.1e100.net (172.217.26.46)  8.965 ms  9.341 ms  10.773 ms
 
 # traceroute -T google.com	>> Uses TCP instead of UDP packets when default traceroute is blocked or filtered
traceroute to google.com (172.217.26.46), 30 hops max, 60 byte packets
 1  DESKTOP-CPK0PUB.mshome.net (172.19.96.1)  2.365 ms  10.642 ms *
 2  192.168.1.1 (192.168.1.1)  2.473 ms * *
 3  10.105.61.1 (10.105.61.1)  6.481 ms * *
 4  * * *
 5  * * *
 6  103.44.18.21 (103.44.18.21)  8.789 ms  8.015 ms  8.333 ms
 7  142.251.77.27 (142.251.77.27)  8.625 ms 142.251.77.23 (142.251.77.23)  5.998 ms 142.251.77.27 
 
 # dig google.com		>> - Retrieves the default DNS record (usually an A record) and Confirms the IP address associated with a domain.
; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 53090
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;google.com.                    IN      A

;; ANSWER SECTION:
google.com.             283     IN      A       172.217.26.46

;; Query time: 39 msec
;; SERVER: 10.255.255.254#53(10.255.255.254) (UDP)
;; WHEN: Sat Mar 07 02:53:45 UTC 2026
;; MSG SIZE  rcvd: 55

# dig -x google.com		>> Check Reverse DNS (PTR Records). Useful for verifying mail server configurations
;; communications error to 10.255.255.254#53: timed out
;; communications error to 10.255.255.254#53: timed out
;; communications error to 10.255.255.254#53: timed out

; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> -x google.com
;; global options: +cmd
;; no servers could be reached

# dig +noall +answer google.com		>> - Useful for clean, script-friendly results
google.com.             42      IN      A       172.217.26.46

# dig +trace google.com		>> Displays the step-by-step resolution from root servers down to authoritative servers, Excellent for diagnosing complex DNS problems.

; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> +trace google.com
;; global options: +cmd
.                       36025   IN      NS      i.root-servers.net.
.                       36025   IN      NS      l.root-servers.net.
.                       36025   IN      NS      b.root-servers.net.
.                       36025   IN      NS      j.root-servers.net.
.                       36025   IN      NS      m.root-servers.net.
.                       36025   IN      NS      c.root-servers.net.
.                       36025   IN      NS      a.root-servers.net.
.                       36025   IN      NS      d.root-servers.net.
.                       36025   IN      NS      k.root-servers.net.
.                       36025   IN      NS      e.root-servers.net.
.                       36025   IN      NS      f.root-servers.net.
.                       36025   IN      NS      g.root-servers.net.
.                       36025   IN      NS      h.root-servers.net.
.                       36025   IN      RRSIG   NS 8 0 518400 20260319050000 20260306040000 21831 . Uygh0M9al2HP/1DQptFy8qR654PJ+J9BweSqX7KJdXLxW33vSeDUgacf DdWB1547jnw8BdBpuNbkAdCIFMlK/Ow2i+N821/vWB6hMdv7TuhjpRgd lYyqH9kv3812i31FwzbZNSfyyNwnm2z3fnP1RAmy3np9kt9I0MLmnYhx wkd52saVnzRp2kiwFKB+FI7gHx+P9ALONACVH86EoPfO4eWdllugg5o+ 8HAhVkipHAg3Q2RrnkaCvjxj7mbr94UrRr1AeGgsAQY5/Fx8PSFbbWBM qR4ZkGEEzF1Bd33Z9d13FjhpiIdtQ5ByzBzTXCvgHCtYLTBKxtcEViuU OOKlmA==
;; Received 525 bytes from 10.255.255.254#53(10.255.255.254) in 11 ms

google.com.             192     IN      A       172.217.26.46
;; Received 55 bytes from 192.112.36.4#53(g.root-servers.net) in 7 ms

- Command is one of the most versatile tools for interacting with URLs and transferring data. it is widely used for testing APIs, downloading files.
Example:
# curl -O https://example.com/file.zip
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   528    0   528    0     0   3728      0 --:--:-- --:--:-- --:--:--  3718
# ls -l
total 8
drwxr-xr-x 4 root root 4096 Mar  5 01:33 DevOps
-rw-r--r-- 1 root root  528 Mar  7 03:04 file.zip

- wget : The command is a powerful utility for non-interactive downloading of files from the web. It’s especially useful for automation, scripting, and handling large or recursive downloads.

Example:
# wget https://example.com/file.zip		>> Fetches the file and saves it locally
--2026-03-07 03:10:36--  https://example.com/file.zip
Resolving example.com (example.com)... 104.18.26.120, 104.18.27.120, 2606:4700::6812:1a78, ...
Connecting to example.com (example.com)|104.18.26.120|:443... connected.

# wget -c https://example.com/largefile.iso >> Use it Continues (Interrupted) downloading from where it left off

# wget -i urls.txt(listed multiple usrl for multiple files) >> Reads a list of URLs from a file and downloads them all.

# wget -b https://example.com/largefile.iso >> Download in Background and logs progress to a file

# wget --limit-rate=200k https://example.com/file.zip	>> Limit Download Speed to avoid hogging bandwidth.
