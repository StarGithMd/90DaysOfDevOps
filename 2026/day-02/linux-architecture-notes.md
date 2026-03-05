# Introduction to Linux

## 🖥️ Unix Overview
- Unix is a commercial operating system consisting of **Kernel, Shell, and Programs**.  
- Originally developed in the 1970s, written in **C programming language**.  
- Features:
  - Multiuser  
  - Multitasking  
  - Flexible and adaptable  

---

## 🏗️ Unix Architecture Layers
1. **User** → Person interacting with the OS (e.g., humans).  
2. **System Hardware** → Input/output devices (keyboard, monitor).  
3. **Kernel** → Core of the OS, manages files, security, network, I/O devices, memory, and processes.  
4. **Shell** → Interface between user and kernel, created after login authentication.  

---

## 🐧 Linux Overview
- Linux is an **open-source Unix-like OS** developed by **Linus Torvalds**.  
- Source code is freely available for modification and contribution.  
- Known for **stability, security, and flexibility**.  
- Used in smartphones, laptops, servers, and supercomputers.  
- Popular distributions: **Ubuntu, Fedora, Debian, CentOS**.  

---

## ⌨️ Popular Linux Shortcut Keys
- `Alt + F2` → Open Gnome terminal  
- `Alt + F10` → Maximize window  
- `Alt + F5` → Minimize window  
- `Ctrl + Shift + +` → Increase font  
- `Ctrl + -` → Decrease font  
- `Ctrl + Shift + N` → New terminal  
- `Ctrl + Shift + T` → New sub-terminal  
- `Ctrl + PgUp/PgDn` → Move cursor in terminal  
- `Ctrl + D` → Exit terminal  
- `Alt + F4` → Close terminal  
- `Ctrl + A` → Move cursor to beginning of line  
- `Ctrl + E` → Move cursor to end of line  
- `Ctrl + U` → Delete before cursor  
- `Ctrl + K` → Delete after cursor  
- `Up Arrow` → Recall last command  
- `!!` → Repeat last command  
- `!5` → Run 5th command from history  
- `!-5` → Run 5th last command from history  
- `Ctrl + R` → Search command history  

---

## 🔠 Meta Characters in Linux
- `*` → Matches zero or more characters (`ls *.txt`)  
- `?` → Matches a single character (`ls ???.*`)  
- `[ ]` → Matches any character inside brackets (`ls [a,b,c]*`)  
- `-` → Range of characters (`ls [a-z]*`)  
- `{ }` → Brace expansion (`mkdir {dir1,dir2,dir3}`)  
- `~` → Home directory (`cd ~`)  
- `.` → Current directory (`ls .`)  
- `$` → Variable expansion (`echo $myvar`)  
- `&` → Run command in background (`mycommand &`)  
- `|` → Pipe output (`ls | sort`)  
- `>` → Redirect output (overwrite)  
- `>>` → Redirect output (append)  
- `<` → Redirect input  
- `;` → Run multiple commands (`ls -l; df -h`)  

---

## 📋 Popular Linux Commands
- Basic: `ls`, `touch`, `cat`, `df`, `echo`, `vi`, `vim`, `rm`, `mv`  
- Viewing: `tac`, `nl`, `less`, `more`, `tail`, `head`, `wc`  
- Searching: `grep`, `egrep`, `fgrep`  
- Sorting: `sort`, `diff`, `uniq`  
- Processing: `cut`, `awk`, `sed`, `fmt`, `find`  

---

## ⚡ Advanced Linux Commands
### cut
- `cut -c1 /etc/passwd` → First character  
- `cut -c1,3 /etc/passwd` → Characters 1 and 3  
- `cut -c1-5 /etc/passwd` → Range 1–5  
- `cut -b 1 myfile.txt` → First byte  
- `cut -d':' -f1 /etc/passwd` → First field using delimiter  

### sed
- `sed -n '1p' /etc/passwd` → Print first line  
- `sed 's/root/network/g' file` → Replace text globally  
- `sed -i 's/root/network/g' file` → Replace text in file (persistent)  
- `sed '5i hello' file` → Insert before line 5  
- `sed '5a hello' file` → Append after line 5  

### awk
- `df -h | awk '{print $1, $2}' | column -t` → Print columns  
- `ifconfig | grep inet | awk '{print $2}'` → Extract IP address  
- `tail -5 /etc/passwd | awk -F':' '{print $1,$6}'` → Print username and home directory  

---

## 🔗 Links
- **Hard Link** → Same inode, file only  
- **Soft Link** → Different inode, supports directories and files across partitions  

---

## 🌐 Networking (nmcli)
- `nmcli connection show` → Show connections  
- `nmcli connection delete ens33` → Delete connection  
- `nmcli connection add con-name ens33 ifname ens33 type ethernet autoconnect yes ipv4 192.168.10.10/24` → Add connection  

---

## 📊 File & Directory Utilities
- `sort file` → Sort contents  
- `diff file1 file2` → Compare files  
- `wc file` → Word/line count  
