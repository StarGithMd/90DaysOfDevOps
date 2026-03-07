## Day 07 – Linux File System Hierarchy & Scenario-Based Practice
 - Today's goal is to understand where things live in Linux and practice troubleshooting
 
 - Part 1: Linux File System Hierarchy (30 minutes)
 
## The Linux filesystem hierarchy is organized under the root directory /, with several critical subdirectories defined by the Filesystem Hierarchy Standard (FHS).

- /boot		: Boot loader file	(Kernel images and boot configs, grub).
- /bin		: Essential user binaries (basic commands ls, cp, mv, cat' Needed for system boot.
- /sbin		: System binaries (Commands for system administration 'hutdown, mount').
- / (Root)	: The top-level directory (All files and directories branch from here).
- /etc		: Configuration file (Stores system-wide config files /etc/passwd, /etc/fstab).
- /home		: User home directories (Each user gets a personal directory /home/md).
- /root		: Root user’s home (Equivalent to /home but for the superuser).
- /var		: Variable data (Logs (/var/log), mail, spool files. Changes frequently).
- /usr		: User applications (Contains most installed software, libraries, documentation). 
- /opt		: Optional software	(Third-party or add-on packages).
- /mnt & /media: Mount points (Used for mounting external drives, CDs, USBs). 
- /dev		: Device file (Represents hardware devices , /dev/sda for disks).
- /tmp		: Temporary files (Used by applications for short-term storage. Cleared on reboot).

## Write 1-2 lines explaining what it contains
# ls -l
drwxr-xr-x  22 root root    4096 Mar  7 06:42 .
drwxr-xr-x   2 root root    4096 Apr 22  2024 boot
lrwxrwxrwx   1 root root       7 Apr 22  2024 bin -> usr/bin
lrwxrwxrwx   1 root root       8 Apr 22  2024 sbin -> usr/sbin
drwxr-xr-x  89 root root    4096 Mar  7 09:46 etc
drwxr-xr-x   2 root root    4096 Apr 22  2024 home
drwx------   8 root root    4096 Mar  7 10:30 root
drwxr-xr-x  13 root root    4096 Mar  4 01:07 var
drwxr-xr-x  12 root root    4096 Jan  6  2025 usr
drwxr-xr-x   2 root root    4096 Jan  6  2025 opt
drwxr-xr-x   2 root root    4096 Jan  6  2025 media
drwxr-xr-x  15 root root    3860 Mar  7 06:42 dev
drwxrwxrwt   8 root root    4096 Mar  7 10:28 tmp

# ls -al /boot
total 8
drwxr-xr-x  2 root root 4096 Apr 22  2024 .
drwxr-xr-x 22 root root 4096 Mar  7 06:42 ..
# ls -al /bin
lrwxrwxrwx 1 root root 7 Apr 22  2024 /bin -> usr/bin
# ls -al /sbin
lrwxrwxrwx 1 root root 8 Apr 22  2024 /sbin -> usr/sbin
# ls -al /etc
total 796
drwxr-xr-x 89 root root       4096 Mar  7 09:46 .
drwxr-xr-x 22 root root       4096 Mar  7 06:42 ..
-rw-------  1 root root          0 Jan  6  2025 .pwd.lock
# ls -al /etc |wc
    168    1519    9790
# ls -al /home
total 8
drwxr-xr-x  2 root root 4096 Apr 22  2024 .
drwxr-xr-x 22 root root 4096 Mar  7 06:42 ..
# ls -l /root
total 8
drwxr-xr-x 5 root root 4096 Mar  7 10:02 DevOps
# ls -l /var
total 44
drwxr-xr-x  2 root root   4096 Mar  7 03:15 backups
drwxr-xr-x 13 root root   4096 Mar  4 01:07 cache
drwxrwsrwt  2 root root   4096 Jan  6  2025 crash
drwxr-xr-x 32 root root   4096 Jan  6  2025 lib
drwxrwsr-x  2 root staff  4096 Apr 22  2024 local
lrwxrwxrwx  1 root root      9 Jan  6  2025 lock -> /run/lock
drwxrwxr-x  9 root syslog 4096 Mar  7 09:08 log
drwxrwsr-x  2 root mail   4096 Jan  6  2025 mail
drwxr-xr-x  2 root root   4096 Jan  6  2025 opt
lrwxrwxrwx  1 root root      4 Jan  6  2025 run -> /run
drwxr-xr-x  8 root root   4096 Mar  7 08:27 snap
drwxr-xr-x  4 root root   4096 Jan  6  2025 spool
drwxrwxrwt  7 root root   4096 Mar  7 10:48 tmp

# ls -l /usr
total 80
drwxr-xr-x   2 root root 36864 Mar  7 09:08 bin
drwxr-xr-x   2 root root  4096 Apr 22  2024 games
drwxr-xr-x   4 root root  4096 Mar  7 06:47 include
drwxr-xr-x  56 root root  4096 Mar  7 09:08 lib
drwxr-xr-x   2 root root  4096 Mar  7 06:46 lib64
drwxr-xr-x   7 root root  4096 Mar  7 07:16 libexec
drwxr-xr-x  10 root root  4096 Jan  6  2025 local
drwxr-xr-x   2 root root 12288 Mar  7 07:16 sbin
drwxr-xr-x 109 root root  4096 Mar  7 07:16 share
drwxr-xr-x   2 root root  4096 Apr 22  2024 src

# ls -l /opt
total 0
# ls -l /dev
total 0
crw-r--r-- 1 root root     10, 235 Mar  7 06:42 autofs
drwxr-xr-x 2 root root         600 Mar  7 06:42 block
drwxr-xr-x 2 root root         120 Mar  7 06:42 bsg

# ls -l /dev |wc
    192    1908   10470

## Hands-on task:
## Find the largest log file in /var/log
# du -sh /var/log/* 2>/dev/null | sort -h | tail -5
344K    /var/log/kern.log
356K    /var/log/apt
528K    /var/log/dpkg.log
1.3M    /var/log/syslog
127M    /var/log/journal

## Look at a config file in /etc
# cat /etc/hostname
DESKTOP-CPK0PUB

## Check your home directory
# ls -la ~
total 72
drwx------  8 root root 4096 Mar  7 10:30 .
drwxr-xr-x 22 root root 4096 Mar  7 06:42 ..
-rw-------  1 root root 9177 Mar  7 09:46 .bash_history
-rw-r--r--  1 root root 3106 Apr 22  2024 .bashrc
drwx------  2 root root 4096 Mar  4 01:07 .cache
drwx------  3 root root 4096 Mar  5 02:49 .config
-rw-r--r--  1 root root   54 Mar  4 04:46 .gitconfig
-rw-------  1 root root   20 Mar  7 10:30 .lesshst
drwxr-xr-x  3 root root 4096 Mar  4 03:43 .local
-rw-r--r--  1 root root    0 Mar  7 01:04 .motd_shown
-rw-r--r--  1 root root  161 Apr 22  2024 .profile
drwx------  2 root root 4096 Jan  6  2025 .ssh
-rw-------  1 root root 9706 Mar  7 09:54 .viminfo
drwxr-xr-x  5 root root 4096 Mar  7 10:02 DevOps
drwx------  3 root root 4096 Mar  7 08:27 snap

## Part 2: Scenario-Based Practice (40 minutes)
## Question: How do you check if the 'nginx' service is running?

# apt install nginx					>> First deploy the nginx package on it.

## Step 1: Check service status
# systemctl status nginx
● nginx.service - A high performance web server and a reverse proxy ser>
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; pr>
     Active: active (running) since Sat 2026-03-07 10:58:05 UTC; 52s ago
       Docs: man:nginx(8)
    Process: 18834 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; mas>
    Process: 18835 ExecStart=/usr/sbin/nginx -g daemon on; master_proce>
   Main PID: 18870 (nginx)
      Tasks: 9 (limit: 9151)
     Memory: 6.4M (peak: 14.3M)
        CPU: 127ms
     CGroup: /system.slice/nginx.service

## Step 2: If service is not found, list all services
# systemctl list-units --type=service |grep nginx
  nginx.service                            loaded active     running      A high performance web server and a reverse proxy server
  
## Step 3: Check if service is enabled on boot
# systemctl is-enabled nginx
enabled

# journalctl -u nginx -n 50
Mar 07 10:58:05 DESKTOP-CPK0PUB systemd[1]: Starting nginx.service - A >
Mar 07 10:58:05 DESKTOP-CPK0PUB systemd[1]: Started nginx.service - A h>
lines 1-2/2 (END)

## Your manager reports that the application server is slow.
A. first we should check the server resource utilization like, CPU, Mrmory, and Disk space and performance.

## You SSH into the server. What commands would you run to identify
A. Check service for running status "systemctl status ssh" , system sould be reachable and accessible. check for open port.
## which process is using high CPU?
A. Check command ps. top, ptop to see the real time proces utolization.

# top
top - 11:06:14 up  4:30,  1 user,  load average: 0.03, 0.01, 0.00
Tasks:  42 total,   1 running,  41 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   7636.2 total,   6858.4 free,    587.5 used,    360.6 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   7048.7 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
  19021 root      20   0    9272   5504   3456 R   3.3  0.1   0:00.13 top
  
## there is top cammand getting more CPU consumption and memory also.

## Scenario 3: Finding Service Logs
## A developer asks: "Where are the logs for the 'docker' service?"
A. Generally linux saved log under directory /var/log/docker.
## The service is managed by systemd.
A. systemctl status docker
## What commands would you use?
A. journalctl -k, journalctl -u docker

## Check service status first
# systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: enabled)
     Active: active (running) since Sat 2026-03-07 11:26:25 UTC; 6s ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 19849 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
   Main PID: 19851 (sshd)
      Tasks: 1 (limit: 9151)
     Memory: 1.2M (peak: 1.6M)
        CPU: 44ms
     CGroup: /system.slice/ssh.service
	 
## View last 50 lines of logs
# journalctl -u ssh -n 50
Mar 07 11:26:25 DESKTOP-CPK0PUB systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
Mar 07 11:26:25 DESKTOP-CPK0PUB sshd[19851]: Server listening on 0.0.0.0 port 22.
Mar 07 11:26:25 DESKTOP-CPK0PUB sshd[19851]: Server listening on :: port 22.
Mar 07 11:26:25 DESKTOP-CPK0PUB systemd[1]: Started ssh.service - OpenBSD Secure Shell server.

## Follow logs in real-time
# journalctl -u ssh -f
Mar 07 11:26:25 DESKTOP-CPK0PUB systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
Mar 07 11:26:25 DESKTOP-CPK0PUB sshd[19851]: Server listening on 0.0.0.0 port 22.
Mar 07 11:26:25 DESKTOP-CPK0PUB sshd[19851]: Server listening on :: port 22.
Mar 07 11:26:25 DESKTOP-CPK0PUB systemd[1]: Started ssh.service - OpenBSD Secure Shell server.

## Scenario 4: File Permissions Issue

## A script at /root/DevOp/backup.sh not executing.
## When you run it: ./backup.sh
## You get: "Permission denied"

## What commands would you use to fix this?
# chmod +x /root/DevOp/backup.sh

# we also can run without giving x permition using "bash /root/DevOp/backup.sh"

## Step-by-step solution structure:
## Step 1: Check current permissions
# ls -l # ls -l /root/DevOp/backup.sh
-rw-r--r-- 1 root root   21 Mar  7 10:03	backup.sh	>> Noticed no 'x' = not executable.

## Step 2: Add execute permission
# chmod +x /root/DevOp/backup.sh

## Step 3: Verify it worked
# ls -l /root/DevOp/backup.sh
-rwxr--r-- 1 root root   21 Mar  7 10:03	/root/DevOp/backup.sh	>> Noticed 'x' permission for executable is availble
