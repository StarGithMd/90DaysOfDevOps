## Day 05 – Linux Troubleshooting Drill: CPU, Memory, and Logs

- Capture a quick health snapshot (CPU, memory, disk, network)

# top -n 1 | head -n 10
top - 09:07:11 up  2:28,  1 user,  load average: 0.00, 0.02, 0.04
Tasks:  39 total,   1 running,  38 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   7636.2 total,   6973.0 free,    587.7 used,    245.3 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   7048.5 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
      1 root      20   0   22308  13184   9600 S   0.0   0.2   0:06.95 systemd
      2 root      20   0    3120   1920   1920 S   0.0   0.0   0:00.01 init-sy+
      7 root      20   0    3136   1792   1792 S   0.0   0.0   0:00.00 init
  
# mpstat 1 1
Linux 6.6.87.2-microsoft-standard-WSL2 (DESKTOP-CPK0PUB)        03/07/26        _x86_64_        (8 CPU)

09:08:44     CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle
09:08:45     all    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00  100.00
Average:     all    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00  100.00

# free -h              
			Total        used        free      shared  buff/cache   available
Mem:        7.5Gi       583Mi       6.8Gi       3.9Mi       248Mi       6.9Gi
Swap:       2.0Gi          0B       2.0Gi

# vmstat 1 5
procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu
 0  0      0 7138064   1708 253268    0    0   250   435  244    0  0  0 99  0  0  0
 0  0      0 7138064   1708 253424    0    0     0     0   42   47  0  0 100  0  0  0
 1  0      0 7138064   1708 253424    0    0     0     0   43   50  0  0 100  0  0  0
 1  0      0 7138064   1708 253424    0    0     0     0   28   35  0  0 100  0  0  0
 0  0      0 7138064   1708 253424    0    0     0     0   38   60  0  0 100  0  0  0
 
 # df -hT
Filesystem     Type           Size  Used Avail Use% Mounted on
none           overlay        3.8G     0  3.8G   0% /usr/lib/modules/6.6.87.2-microsoft-standard-WSL2
none           tmpfs          3.8G  4.0K  3.8G   1% /mnt/wsl
drivers        9p             220G  111G  109G  51% /usr/lib/wsl/drivers
/dev/sdd       ext4          1007G  2.9G  953G   1% /
none           tmpfs          3.8G  112K  3.8G   1% /mnt/wslg
none           overlay        3.8G     0  3.8G   0% /usr/lib/wsl/lib
rootfs         rootfs         3.8G  2.7M  3.8G   1% /init
none           tmpfs          3.8G  624K  3.8G   1% /run
none           tmpfs          3.8G     0  3.8G   0% /run/lock
none           tmpfs          3.8G     0  3.8G   0% /run/shm
none           overlay        3.8G   76K  3.8G   1% /mnt/wslg/versions.txt
none           overlay        3.8G   76K  3.8G   1% /mnt/wslg/doc

# du -sh /var/log/*
32K     /var/log/alternatives.log
24K     /var/log/auth.log
116K    /var/log/bootstrap.log
10.0k	/var/log/nginx/error.log
4.0K    /var/log/syslog
10.0k	/var/log/messages
36K     /var/log/dmesg

# journalctl -k
Mar 07 06:42:32 DESKTOP-CPK0PUB kernel: Linux version 6.6.87.2-microsoft-standard-WSL2 (root@439a258ad544) (gcc (GCC) 11.2.>
Mar 07 06:42:32 DESKTOP-CPK0PUB kernel: Command line: initrd=\initrd.img WSL_ROOT_INIT=1 panic=-1 nr_cpus=8 hv_utils.timesy>
Mar 07 06:42:32 DESKTOP-CPK0PUB kernel: KERNEL supported cpus:
Mar 07 06:42:32 DESKTOP-CPK0PUB kernel:   Intel GenuineIntel
Mar 07 06:42:32 DESKTOP-CPK0PUB kernel:   AMD AuthenticAMD
Mar 07 06:42:32 DESKTOP-CPK0PUB kernel: BIOS-provided physical RAM map:

# journalctl -p err
Mar 04 01:07:34 DESKTOP-CPK0PUB kernel: PCI: Fatal: No config space access function found
Mar 04 01:07:34 DESKTOP-CPK0PUB kernel: misc dxg: dxgk: dxgkio_is_feature_enabled: Ioctl failed: -22
Mar 04 01:07:34 DESKTOP-CPK0PUB kernel: misc dxg: dxgk: dxgkio_query_adapter_info: Ioctl failed: -22
Mar 04 01:07:34 DESKTOP-CPK0PUB kernel: misc dxg: dxgk: dxgkio_query_adapter_info: Ioctl failed: -22
Mar 04 01:07:34 DESKTOP-CPK0PUB kernel: misc dxg: dxgk: dxgkio_query_adapter_info: Ioctl failed: -22
Mar 04 01:07:34 DESKTOP-CPK0PUB kernel: misc dxg: dxgk: dxgkio_query_adapter_info: Ioctl failed: -2
Mar 04 01:07:41 DESKTOP-CPK0PUB login[378]: PAM unable to dlopen(pam_lastlog.so): /usr/lib/security/pam_lastlog.so: cannot >
Mar 04 01:07:41 DESKTOP-CPK0PUB login[378]: PAM adding faulty module: pam_lastlog.so
Mar 04 01:08:20 DESKTOP-CPK0PUB unknown: WSL (218) ERROR: CheckConnection: getaddrinfo() failed: -5
Mar 04 06:11:40 DESKTOP-CPK0PUB systemd[1]: Failed unmounting init.mount - /init.
-- Boot a4c5461105e64d6fb361f609a2d12910 --

# dmesg
[    0.000000] Linux version 6.6.87.2-microsoft-standard-WSL2 (root@439a258ad544) (gcc (GCC) 11.2.0, GNU ld (GNU Binutils) 2.37) #1 SMP PREEMPT_DYNAMIC Thu Jun  5 18:30:46 UTC 2025
[    0.000000] Command line: initrd=\initrd.img WSL_ROOT_INIT=1 panic=-1 nr_cpus=8 hv_utils.timesync_implicit=1 console=hvc0 debug pty.legacy_count=0 WSL_ENABLE_CRASH_DUMP=1
[    0.000000] KERNEL supported cpus:
[    0.000000]   Intel GenuineIntel
[    0.000000]   AMD AuthenticAMD
[    0.000000] BIOS-provided physical RAM map:

# cat /var/log/syslog |grep "error"
2026-03-04T01:07:35.483579+00:00 DESKTOP-CPK0PUB systemd[1]: apport-autoreport.path - Process error reports when automatic reporting is enabled (file watch) was skipped because of an unmet condition check (ConditionPathExists=/var/lib/apport/autoreport).
2026-03-04T01:07:35.483583+00:00 DESKTOP-CPK0PUB systemd[1]: apport-autoreport.timer - Process error reports when automatic reporting is enabled (timer based) was skipped because of an unmet condition check (ConditionPathExists=/var/lib/apport/autoreport).
2026-03-04T01:07:35.636183+00:00 DESKTOP-CPK0PUB snapd[185]: helpers.go:160: error trying to compare the snap system key: system-key missing on disk
grep: (standard input): binary file matches
