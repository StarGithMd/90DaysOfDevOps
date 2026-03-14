
## Day 22 – Introduction to Git: Your First Repository
## Today's goal is to practice user and group management by completing hands-on challenges.

## Today marks the beginning of your Git journey. Git is the backbone of modern DevOps every tool, pipeline, and workflow revolves around version control. Before diving into advanced concepts, you need to get comfortable with the basics by doing.

## Understand what Git is and why it matters
 - A: Version Control System (VCS): Git records changes to files over time, allowing you to revisit or restore earlier versions.
 
## Set up your first Git repository from scratch
 - A: Download Git from git-scm.com and install it.
 
## Task 1: Install and Configure Git
 - Verify Git is installed on your machine
 - Set up your Git identity — name and email
 - Verify your configuration
 
C:\Users\Md Rustam>winget install --id Git.Git -e --source winget
Found an existing package already installed. Trying to upgrade the installed package... 
 
# git --version
git version 2.43.0 

# git -v
git version 2.43.0

# git config --global user.name "Md Rustam"
# git config --global user.email "mdrstm669@gmail.com"
# git config --list
user.name=Md Rustam
user.email=mdrstm669@gmail.com

# pwd
/root/DevOps/demo

# ls -al
total 8
drwxr-xr-x 2 root root 4096 Mar 14 03:08 .
drwxr-xr-x 4 root root 4096 Mar 14 02:45 ..

# git init
# git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:
hint:   git config --global init.defaultBranch <name>

## Task 2: Create Your Git Project
 - Create a new folder called devops-git-practice
 - Initialize it as a Git repository
 - Check the status — read and understand what Git is telling you
 - Explore the hidden .git/ directory — look at what's inside

# mkdir devops-git-practice; cd devops-git-practice
# ls -la
total 8
drwxr-xr-x 2 root root 4096 Mar 14 03:19 .
drwxr-xr-x 5 root root 4096 Mar 14 03:19 ..

# git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:   git config --global init.defaultBranch <name>

# ls -al
total 12
drwxr-xr-x 3 root root 4096 Mar 14 03:20 .
drwxr-xr-x 5 root root 4096 Mar 14 03:19 ..
drwxr-xr-x 7 root root 4096 Mar 14 03:20 .git

# git status
On branch master
No commits yet
nothing to commit (create/copy files and use "git add" to track)

# ls -al .git
total 40
drwxr-xr-x 7 root root 4096 Mar 14 03:21 .
drwxr-xr-x 3 root root 4096 Mar 14 03:20 ..
-rw-r--r-- 1 root root   23 Mar 14 03:20 HEAD
drwxr-xr-x 2 root root 4096 Mar 14 03:20 branches
-rw-r--r-- 1 root root   92 Mar 14 03:20 config
-rw-r--r-- 1 root root   73 Mar 14 03:20 description
drwxr-xr-x 2 root root 4096 Mar 14 03:20 hooks
drwxr-xr-x 2 root root 4096 Mar 14 03:20 info
drwxr-xr-x 4 root root 4096 Mar 14 03:20 objects
drwxr-xr-x 4 root root 4096 Mar 14 03:20 refs

## Task 3: Create Your Git Commands Reference
 - Create a file called git-commands.md inside the repo
 
 # Add the Git commands you've used so far, organized by category:
 - Setup & Config
 - Basic Workflow
 - Viewing Changes
 
 # For each command, write:
 - What it does (1 line)
 - An example of how to use it
 
# touch git-commands.md; # ls -l
total 0
-rw-r--r-- 1 root root 0 Mar 14 03:28 git-commands.md

# ls -la		
total 12
drwxr-xr-x 3 root root 4096 Mar 14 03:28 .
drwxr-xr-x 5 root root 4096 Mar 14 03:19 ..
drwxr-xr-x 7 root root 4096 Mar 14 03:21 .git
-rw-r--r-- 1 root root    0 Mar 14 03:28 git-commands.md

# git config --list
user.name=Md Rustam
user.email=mdrstm669@gmail.com

# # git add git-commands.md; # git status
On branch master
No commits yet
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   git-commands.md

# git rm --cached git-commands.md
rm 'git-commands.md'

# git status
On branch master
No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        git-commands.md

nothing added to commit but untracked files present (use "git add" to track)

# git add git-commands.md; 
# git status
On branch master
No commits yet
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   git-commands.md

# git commit -m 'added 1st file'
[master (root-commit) 8fddd8c] added 1st file
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 git-commands.md
 
# git status
On branch master
nothing to commit, working tree clean

# git log --oneline
8fddd8c (HEAD -> master) added 1st file

# git show
commit 8fddd8c1b63d45b5431180504349698775350bac (HEAD -> master)
Author: Md Rustam <mdrstm669@gmail.com>
Date:   Sat Mar 14 03:35:17 2026 +0000
    added 1st file
diff --git a/git-commands.md b/git-commands.md
new file mode 100644
index 0000000..e69de29

# ls -la
total 12
drwxr-xr-x 3 root root 4096 Mar 14 03:28 .
drwxr-xr-x 5 root root 4096 Mar 14 03:19 ..
drwxr-xr-x 8 root root 4096 Mar 14 03:35 .git
-rw-r--r-- 1 root root    0 Mar 14 03:28 git-commands.md

# ls -la .git
total 52
drwxr-xr-x 8 root root 4096 Mar 14 03:35 .
drwxr-xr-x 3 root root 4096 Mar 14 03:28 ..
-rw-r--r-- 1 root root   15 Mar 14 03:35 COMMIT_EDITMSG
-rw-r--r-- 1 root root   23 Mar 14 03:20 HEAD
drwxr-xr-x 2 root root 4096 Mar 14 03:20 branches
-rw-r--r-- 1 root root   92 Mar 14 03:20 config
-rw-r--r-- 1 root root   73 Mar 14 03:20 description
drwxr-xr-x 2 root root 4096 Mar 14 03:20 hooks
-rw-r--r-- 1 root root  145 Mar 14 03:35 index
drwxr-xr-x 2 root root 4096 Mar 14 03:20 info
drwxr-xr-x 3 root root 4096 Mar 14 03:35 logs
drwxr-xr-x 7 root root 4096 Mar 14 03:35 objects
drwxr-xr-x 4 root root 4096 Mar 14 03:20 refs

## Task 4: Stage and Commit
 - Stage your file
 - Check what's staged
 - Commit with a meaningful message
 - View your commit history
 
# echo "These are common Git commands used in various situations" > git-commands.md
# git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   git-commands.md
no changes added to commit (use "git add" and/or "git commit -a")

# git log --oneline
8fddd8c (HEAD -> master) added 1st file

# git show
commit 8fddd8c1b63d45b5431180504349698775350bac (HEAD -> master)
Author: Md Rustam <mdrstm669@gmail.com>
Date:   Sat Mar 14 03:35:17 2026 +0000
    added 1st file

diff --git a/git-commands.md b/git-commands.md
new file mode 100644
index 0000000..e69de29

# # git add .; git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   git-commands.md

# git commit -m 'basic command added'
[master 3d4b09d] basic command added
 1 file changed, 17 insertions(+)
 
# git status
On branch master
nothing to commit, working tree clean

# git log
commit 3d4b09d3d6e6f17259879a8cb78dae8c8a775fda (HEAD -> master)
Author: Md Rustam <mdrstm669@gmail.com>
Date:   Sat Mar 14 04:01:01 2026 +0000
    basic command added

commit 8fddd8c1b63d45b5431180504349698775350bac
Author: Md Rustam <mdrstm669@gmail.com>
Date:   Sat Mar 14 03:35:17 2026 +0000
    added 1st file
	
# git log --oneline
3d4b09d (HEAD -> master) basic command added
8fddd8c added 1st file

# git show
commit 3d4b09d3d6e6f17259879a8cb78dae8c8a775fda (HEAD -> master)
Author: Md Rustam <mdrstm669@gmail.com>
Date:   Sat Mar 14 04:01:01 2026 +0000
    basic command added

diff --git a/git-commands.md b/git-commands.md
index e69de29..ea4bb39 100644
--- a/git-commands.md
+++ b/git-commands.md
@@ -0,0 +1,17 @@

## Task 5: Make More Changes and Build History
 - Edit git-commands.md — add more commands as you discover them
 - Check what changed since your last commit
 - Stage and commit again with a different, descriptive message
 - Repeat this process at least 3 times so you have multiple commits in your history
 - View the full history in a compact format

# git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   git-commands.md
no changes added to commit (use "git add" and/or "git commit -a")
 
# git add .;# git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   git-commands.md

# git commit -m 'added more commands'
[master ac0f7ff] added more commands
 1 file changed, 6 insertions(+)
 
# git status
On branch master
nothing to commit, working tree clean

# git log
commit ac0f7ff974521847b8c1607fbf1babc465ce866d (HEAD -> master)
Author: Md Rustam <mdrstm669@gmail.com>
Date:   Sat Mar 14 04:13:57 2026 +0000
    added more commands

commit 3d4b09d3d6e6f17259879a8cb78dae8c8a775fda
Author: Md Rustam <mdrstm669@gmail.com>
Date:   Sat Mar 14 04:01:01 2026 +0000
    basic command added

commit 8fddd8c1b63d45b5431180504349698775350bac
Author: Md Rustam <mdrstm669@gmail.com>
Date:   Sat Mar 14 03:35:17 2026 +0000
    added 1st file

# git log --oneline
ac0f7ff (HEAD -> master) added more commands
3d4b09d basic command added
8fddd8c added 1st file

# git show
commit ac0f7ff974521847b8c1607fbf1babc465ce866d (HEAD -> master)
Author: Md Rustam <mdrstm669@gmail.com>
Date:   Sat Mar 14 04:13:57 2026 +0000
    added more commands

diff --git a/git-commands.md b/git-commands.md
index ea4bb39..0f13f3d 100644
--- a/git-commands.md
+++ b/git-commands.md
@@ -15,3 +15,9 @@ These are common Git commands used in various situations
 ## Viewing Changes and status
 - **git status**    >> Shows the status of files (staged, modified, untracked)

+## Main Porcelain Commands
+- **git add .**     >>> Add file contents to the index
+- **git commit**    >>> Record changes to the repository
+- **git  branch**     >>> List, create, or delete branches
+- ** git checkout**     >>> Switch branches or restore working tree files
+- ** git switch**       >>> Switch branches

## Task 6: Understand the Git Workflow
 - Answer these questions in your own words (add them to a day-22-notes.md file):
	- What is the difference between git add and git commit?
	- A: git add command sends the file status to staging area but not active for tracking, git commit command sends file status to tracking area or repository that keep the file under tracking.
	
	- What does the staging area do? Why doesn't Git just commit directly?
	- A: in staging we can edit/modify many and multiple time, but commit one bu one with the genue comment
	
	- What information does git log show you?
	- A: the git log command display commit id, auther and commit date & time
	  # git log
	  commit ac0f7ff974521847b8c1607fbf1babc465ce866d (HEAD -> master)
	  Author: Md Rustam <mdrstm669@gmail.com>
	  Date:   Sat Mar 14 04:13:57 2026 +0000
	  
	- What is the .git/ folder and what happens if you delete it?
	- A: The hiden directory ".git" keeps all contains configuration, metadata and history that makes Git work. once it  accidentally deleted then lose all the records like tracking and configuration setting history.
	
	- What is the difference between a working directory, staging area, and repository?
	- A: The working directory and staging area both are working directory created on filesystem where file create, edit, modify and delete those are out of tracked.

