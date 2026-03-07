Day 02 – Linux Architecture, Processes, and systemd
- Linux architecture is a layered design consisting of hardware, kernel, shell, user space and application layers and Utilities.

Linux Overview
- Linux is an open-source Unix-like OS developed by Linus Torvalds. Source code is freely available for modification and contribution Known for stability, security, and flexibility.
- Used in smartphones, laptops, servers, and supercomputers. Popular distributions: Ubuntu, Fedora, Debian, CentOS

Key Components of Linux Architecture:
- Hardware Layer: The physical devices (CPU, memory, storage, and peripherals) Provides the foundation on which the operating system runs.
- Kernel Layer: The heart of Linux, responsible for managing hardware and system resources (Process, Memory, Device, File system management). It works as mediater in between hardware and software.
- Init/System: This is the first process started by the kernel after booting. Systemd is the modern replacement for traditional init.
- User Space: The environment where applications and user processes run (System libraries, User applications 'Bash, Firefox')
- Shell Layer: Command interpreter that allows users to interact with the kernel. CLI shells (e.g., Bash, Zsh), - GUI shells (GNOME, KDE).
- Application Layer: Application programs and utilities that run on top of the shell that provides functionality for end-users and developers (text editors, browsers, compilers, and system tools).

Systemd is the modern init system in Linux that boots the system, manages services, and controls resources. It matters because it improves boot speed, ensures reliable service management, and provides centralized tools for monitoring and controlling processes.
- systemctl: Unified commands to control services, targets, and system states. Consistent interface across distributions (Ubuntu, Fedora, Arch, Debian, etc.).

Linux servers usually handle processes in different states depending on resource availability. 

There are the main process states in Linux.
- Running : actively executing,identify with 'R', Compiler running.
- Interruptible Sleep : waiting for resources/events, identify with 'S', Text editor waiting for input
- Uninterruptible Sleep : Waiting for I/O, cannot be interrupted, identify with 'D', Disk read/write
- Stopped : paused by a signal, identify with 'T', Program halted with Ctrl+Z
- Zombie : terminated but not cleaned up, identify with 'Z', Child process not reaped.

The top program provides a dynamic real-time view of a running Linux system process.
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
- systemctl : Ssystemd, init, systemd system and service manager

# systemctl status cron			>> shows whether it’s active, failed, or inactive.
 cron.service - Regular background program processing daemon
     Loaded: loaded (/usr/lib/systemd/system/cron.service; enabled; preset: enabled)
     Active: active (running) since Sat 2026-03-07 06:42:32 UTC; 18min ago
       Docs: man:cron(8)
   Main PID: 169 (cron)
      Tasks: 1 (limit: 9151)
     Memory: 408.0K (peak: 1.5M)
        CPU: 10ms
     CGroup: /system.slice/cron.service
             └─169 /usr/sbin/cron -f -P
			 
# systemct reload cron 			>> Reloads configuration without downtime (if supported).
