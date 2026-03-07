## Day 04- Linux Practice: Processes and Services

## let’s get hands-on with Linux fundamentals using real commands to build confidence in navigating, managing files, and controlling processes.

##  Basic Navigation commands (pwd, ls, cd, cd .., cd ~, cd -)
## pwd - Print name of current/working directory
# pwd
/root

## ls - list directory contents
# ls -l /	:  Print file | directort as long list.
total 2796
lrwxrwxrwx   1 root root       7 Apr 22  2024 bin -> usr/bin
drwxr-xr-x   2 root root    4096 Feb 26  2024 bin.usr-is-merged
drwxr-xr-x   2 root root    4096 Apr 22  2024 boot

# cd DevOps/
# pwd
0
# cd ..
# pwd
/root

# cd /
# pwd
# ls -l
total 2796
lrwxrwxrwx   1 root root       7 Apr 22  2024 bin -> usr/bin
drwxr-xr-x   2 root root    4096 Feb 26  2024 bin.usr-is-merged
drwxr-xr-x   2 root root    4096 Apr 22  2024 boot
drwxr-xr-x  15 root root    3860 Mar  7 06:42 dev
drwxr-xr-x  88 root root    4096 Mar  7 07:42 etc

# cd ~
# pwd
root
# cd -
# pwd 
/root/DevOps

## File & Directory Management (touch, vi, vim, nano, mkdir, cp, mv, rm)
# touch day_02_git.md		>> Create an empty file 
# ls -l
-rw-r--r-- 1 root root  156 Mar  4 11:38 day_02_git.md

# mkdir project-1; ls -l		>> Create a new directory
-rw-r--r-- 1 root root  156 Mar  7 01:38 day_02_git.md
drwxr-xr-x 2 root root 4096 Mar  7 08:12 project-1

## See the left first corrector '-' and 'd' that denotes file and directory.
# cp day_02_git.md project-1; ls -l			>> Copy file into directory
drwxr-xr-x 2 root root 4096 Mar  7 08:12 project-1

# cd project-1; ls -l
-rw-r--r-- 1 root root  156 Mar  7 01:38 day_02_git.md

# mv day_02_git.md day_02.md; ls -l		>> Rename or move file
-rw-r--r-- 1 root root  156 Mar  19 01:50 day_02.md

# rm day_02.md; ls -l			>> Delete a file
0

## Permissions & Ownership
# touch new_file.txt; ls -l
-rw-r--r-- 1 root root    0 Mar  7 08:25 new_file.txt		>> View file permissions (rw-r--r-- = 644). r=4, w=2, x=1,
# chmod 644 

## Process Management ( ps, top, kill -9, jobs, fg %1, nohup &)

# ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.1  22104 13184 ?        Ss   06:39   0:06 /usr/
root           2  0.0  0.0   3120  1920 ?        Sl   06:39   0:00 /init
root           7  0.0  0.0   3136  1792 ?        Sl   06:39   0:00 plan9

# firefox
# ps -aux |grep firefox
root       11636  0.2  0.1 451992 12680 ?        Ssl  08:25   0:01 snapfuse /var/lib/snapd/snaps/firefox_7901.snap /snap/firefox/7901 -o ro,nodev,allow_other,suid
root       12720  0.0  0.0   4088  2048 pts/2    S+   08:33   0:00 grep --color=auto firefox

# top
top - 08:35:47 up  1:56,  1 user,  load average: 0.01, 0.08, 0.08
Tasks:  50 total,   1 running,  49 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.1 us,  0.1 sy,  0.0 ni, 99.8 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   7636.2 total,   4789.6 free,    895.9 used,   2128.8 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   6740.3 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
  12732 root      20   0 3142904 319404 159332 S  12.3   4.1   0:05.38 firefox
  
## Pess k botton on with top and type process id of firefox  for kill the firefox. or run the command for same.
# kill -9 12732

# firefox &			>> Run the service & application in background
[1] 14215
root@DESKTOP-CPK0PUB:~# /usr/bin/firefox: 12: xdg-settings: not found
[14215, Main Thread] WARNING: Failed to read portal settings: GDBus.Error:org.freedesktop.DBus.Error.ServiceUnknown: The name org.freedesktop.portal.Desktop was not provided by any .service files: 'glib warning', file /build/firefox/parts/firefox/build/toolkit/xre/nsSigHandlers.cpp:201

or 

# nohup firefox >/dev/null 2>&1 &

# jobs					>> Verify the running firefox service in background.
[1]+  Running                 firefox &

# ps aux | grep firefox
root       11636  0.2  0.1 451992 12536 ?        Ssl  08:24   0:04 snapfuse /var/lib/snapd/snaps/firefox_7901.snap /snap/firefox/7901 -o ro,nodev,allow_other,suid
root       14215 10.6  5.3 3163804 416920 pts/0  Sl   08:51   0:08 /snap/firefox/7901/usr/lib/firefox/firefox

or

# pgrep -l firefox
14215 firefox

or

# pidof firefox
14215 14764

# kill -9 14215			>> close | kill the process.
