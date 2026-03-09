## Day 09 – Linux User & Group Management Challenge
## Today's goal is to practice user and group management by completing hands-on challenges.

## Figure out how to:
- Create users and set passwords
# useradd -m user; passwd user
New password:
Retype new password:
passwd: password updated successfully

- Create groups and assign users
# groupadd groups; usermod -G groups user
# cat /etc/group |grep groups
groups:x:1002:user

- Set up shared directories with group permissions
# mkdir -p /shared/project
# chown :groups /shared/project
# chmod 2770 /shared/project
# ls -ld /shared/project
drwxrws--- 2 root groups 4096 Mar  9 18:44 /shared/project.

## Challenge Tasks
- Task 1: Create Users (20 minutes)
- Create three users with home directories and passwords:
- tokyo
- berlin
- professor

# useradd -m tokyo; useradd -m berlin; useradd -m professor
# tail -3 /etc/passwd
tokyo:x:1002:1003::/home/tokyo:/bin/sh
berlin:x:1003:1004::/home/berlin:/bin/sh
professor:x:1004:1005::/home/professor:/bin/sh 

# passwd tokyo
New password:
Retype new password:
passwd: password updated successfully

# passwd berlin
New password:
Retype new password:
passwd: password updated successfully

# passwd professor
New password:
Retype new password:
passwd: password updated successfully

- Verify: Check /etc/passwd and /home/ directory
# tail -3 /etc/shadow
tokyo:$y$j9T$V4FYdfWnqUIp.UomhYEtF0$SqYibOrkyuNH86y9bdjAYrM0f6Is7XJz3k/eTIkqnmD:20521:0:99999:7:::
berlin:!:20521:0:99999:7:::
professor:!:20521:0:99999:7:::

# find /home -type d -name tokyo -o -name berlin -o -name professor
/home/berlin
/home/professor
/home/tokyo

## Task 2: Create Groups (10 minutes)
- Create two groups:

- developers
- admins
# groupadd developers; groupadd admins

- Verify: Check /etc/group
# tail -2 /etc/group
developers:x:1006:
admins:x:1007:

## Task 3: Assign to Groups (15 minutes)
- Assign users:
- tokyo → developers
- berlin → developers + admins (both groups)
- professor → admins

# usermod -aG developers tokyo berlin
# usermod -aG admins berlin
# usermod -aG admins professor

- Verify: Use appropriate command to check group membership
~# tail -5 /etc/group
tokyo:x:1003:
berlin:x:1004:
professor:x:1005:
developers:x:1006:tokyo,berlin
admins:x:1007:berlin

## Task 4: Shared Directory (20 minutes)
- Create directory: /opt/dev-project
# mkdir -p /opt/dev-project

- Set group owner to developers
# chown :developers /opt/dev-project

- Set permissions to 775 (rwxrwxr-x)
# sudo chmod 775 /opt/dev-project

- Test by creating files as tokyo and berlin
# sudo -u tokyo touch /opt/dev-project/tokyo_test.txt
# sudo -u berlin touch /opt/dev-project/berlin_test.txt

- Verify: Check permissions and test file creation
# ls -ld /opt/dev-project
drwxrwxr-x 2 root developers 4096 Mar  9 19:21 /opt/dev-project

# ls -l /opt/dev-project
total 0
-rw-rw-r-- 1 berlin berlin 0 Mar  9 19:21 berlin_test.txt
-rw-rw-r-- 1 tokyo  tokyo  0 Mar  9 19:21 tokyo_test.txt

## ask 5: Team Workspace (20 minutes)
- Create user nairobi with home directory
# useradd -m nairobi

- Create group project-team
# groupadd project-team

- Add nairobi and tokyo to project-team
# usermod -aG project-team project-team 
- Create /opt/team-workspace directory tokyo

- Set group to project-team, permissions to 775
# chown :project-team /opt/dev-project
# chown 775 project-team

- Test by creating file as nairobi
# sudo -u nairobi touch /opt/dev-project/nairobi_test.txt
# ls -l /opt/dev-project
total 0
-rw-rw-r-- 1 nairobi nairobi 0 Mar  10 19:21 nairobi_test.txt
