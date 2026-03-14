## Day 23 – Git Branching & Working with GitHub
## Now that you know how to create repos, stage, and commit — it's time to learn the most powerful concept in Git: branching. Branches let you work on features, fixes, and experiments in isolation without breaking your main code. You'll also push your work to GitHub for the first time.

## Expected Output
 - A markdown file: day-23-notes.md with your answers
 - Continue updating git-commands.md in your devops-git-practice repo
 - Your practice repo pushed to GitHub
 
## Challenge Tasks: Understanding Branches, The answer is in file. "day-23-notes.md"
 - What is a branch in Git?
 - A: In Git branch is a pointer of comment, where a developers move there topics and comments for new features, bug fixes, or experiments.
 
 - Why do we use branches instead of committing everything to main?
 - A: Branches provides experiment or build features without touching the stable code with isolation. 
 
 - What is HEAD in Git?
 - A: In Git, HEAD is a special pointer that points to the latest commit.

 - What happens to your files when you switch branches?
 - In Git branch is logical bondery where every coment commited into thier branch pointer. whenever switch branch after commited a comment the it will no be vailable with othere brance whatever latest commited before switch.
 
## Task 2: Branching Commands — Hands-On: In your devops-git-practice repo, perform the following:

 - List all branches in your repo
 - Create a new branch called feature-1
 - Switch to feature-1
 - Create a new branch and switch to it in a single command — call it feature-2
 - Try using git switch to move between branches — how is it different from git checkout?
 - Make a commit on feature-1 that does not exist on main
 - Switch back to main — verify that the commit from feature-1 is not there
 - Delete a branch you no longer need
 - Add all branching commands to your git-commands.md
 
 - A: # ls -l
 total 10
 drwxr-xr-x 3 root root 4096 Mar 14 04:10 devops-git-practice

# cd devops-git-practice; ls -al
total 16
drwxr-xr-x 3 root root 4096 Mar 14 04:10 .
drwxr-xr-x 5 root root 4096 Mar 14 03:19 ..
drwxr-xr-x 8 root root 4096 Mar 14 04:14 .git
-rw-r--r-- 1 root root  942 Mar 14 04:10 git-commands.md

# git branch
* master

# git branch feature-1; git branch
  feature-1
* master

# # git switch feature-1; # git branch
* feature-1
  master
  
# # git checkout -b feature-2
Switched to a new branch 'feature-2'

# git branch
  feature-1
* feature-2
  master
  
# git switch feature-1
Switched to branch 'feature-1'

# git branch
* feature-1
  feature-2
  master

# git checkout master
Switched to branch 'master'

# git branch
  feature-1
  feature-2
* master

## git checkout: it is old and used to Multi-functional like switch branches, restore files, or create new branche.
## git switch: it is latest command and used for switching, listing or creating branche.

# git switch feature-1
Switched to branch 'feature-1'

# touch file; echo "this is test file" > file
# ls -l
total 8
-rw-r--r-- 1 root root  18 Mar 14 08:49 file
-rw-r--r-- 1 root root 942 Mar 14 08:49 git-commands.md

# git status
On branch feature-1
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        file

nothing added to commit but untracked files present (use "git add" to track)

# git add .; # git status
On branch feature-1
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   file
		
# git log --oneline
ac0f7ff (HEAD -> feature-1, feature-2) added more commands
3d4b09d basic command added
8fddd8c added 1st file

# git commit -m 'added one line'
[feature-1 82cdb7d] added one line
 1 file changed, 1 insertion(+)
 create mode 100644 file

# git log --oneline
82cdb7d (HEAD -> feature-1) added one line
ac0f7ff (feature-2) added more commands
3d4b09d basic command added
8fddd8c added 1st file

# git show
commit 82cdb7d5de4d8b69893e59472cbc437fb4ea6307 (HEAD -> feature-1)
Author: Md Rustam <mdrstm669@gmail.com>
Date:   Sat Mar 14 08:53:29 2026 +0000

    added one line

diff --git a/file b/file
new file mode 100644
index 0000000..9d8a4e7
--- /dev/null
+++ b/file
@@ -0,0 +1 @@
+this is test file

# git status
On branch master
nothing to commit, working tree clean

# git log
commit e3effcf42f012d1e2166972010098dbda556e8c7 (HEAD -> master)
Author: Md Rustam <mdrstm669@gmail.com>
Date:   Sat Mar 14 08:47:20 2026 +0000

    added branch commands

commit ac0f7ff974521847b8c1607fbf1babc465ce866d (feature-2)
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

# git show
commit e3effcf42f012d1e2166972010098dbda556e8c7 (HEAD -> master)
Author: Md Rustam <mdrstm669@gmail.com>
Date:   Sat Mar 14 08:47:20 2026 +0000

    added branch commands

diff --git a/git-commands.md b/git-commands.md
index 0f13f3d..aa77eae 100644
--- a/git-commands.md
+++ b/git-commands.md
@@ -21,3 +21,31 @@ These are common Git commands used in various situations
 - **git  branch**     >>> List, create, or delete branches
 - ** git checkout**     >>> Switch branches or restore working tree files
 - ** git switch**       >>> Switch branches

# git branch -d feature-2
Deleted branch feature-2 (was ac0f7ff).

# git branch
* master
  feature-1

# git branch -D feature-1
Deleted branch feature-1 (was 82cdb7d).

# git branch
* master

# # git branch --merged
* master


## Task 3: Push to GitHub
 - Create a new repository on GitHub (do NOT initialize it with a README)
 - Connect your local devops-git-practice repo to the GitHub remote
 - Push your main branch to GitHub
 - Push feature-1 branch to GitHub
 - Verify both branches are visible on GitHub
 - Answer in your notes: What is the difference between origin and upstream?

# ls -l
drwxr-xr-x 3 root root 4096 Mar 14 09:15 devops-git-practice

# cd devops-git-practice; ls -l
-rw-r--r-- 1 root root 2351 Mar 14 09:15 git-commands.md

# git branch
  feature-1
  feature-2
* main

# git remote add origin https://github.com/StarGithMd/DebOps_Demo.git
# git remote -v
origin  https://github.com/StarGithMd/DebOps_Demo.git (fetch)
origin  https://github.com/StarGithMd/DebOps_Demo.git (push)

# git push -u origin main
Username for 'https://github.com': StarGithMd
Password for 'https://StarGithMd@github.com':

# ssh-keygen -t ed25519
# cd ~/.ssh; ls -l
total 12
-rw------- 1 root root 411 Mar 14 10:00 id_ed25519
-rw-r--r-- 1 root root 101 Mar 14 10:00 id_ed25519.pub
-rw-r--r-- 1 root root 142 Mar 14 09:51 known_hosts

# cat id_ed25519.pub
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIBCnn5p/w8lg31BdaGj5wlyurUFubahyz7Y2AucN8Vmk mdrstm669@gmail.com

# git push origin main
Enumerating objects: 12, done.
Counting objects: 100% (12/12), done.
Delta compression using up to 8 threads
Compressing objects: 100% (7/7), done.
Writing objects: 100% (12/12), 1.65 KiB | 282.00 KiB/s, done.
Total 12 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), done.
To github.com:StarGithMd/DebOps_Demo.git
 * [new branch]      main -> main

# git push origin main
Everything up-to-date

# git branch -a
  feature-1
  feature-2
* main
  remotes/origin/main
  
# git branch -r
  origin/main
## attached "GitHub_repo" file is a print screen of uploaded local repo to remote repo 
 
## What is the difference between origin and upstream?	
 - A: In Git, “origin” usually refers to fork or personal copy of a repository, the “upstream” refers to the original repository you forked from. They are simply conventional names for remotes.
 - origin: This is default remote pointing to your own fork or clone of a repository, it set automatically when run "git clone or git push origin main".
 - upstream: This is remote pointing to the original source repository (often the one you forked from), it set manually when run "git remote add upstream and git fetch upstream".

## Task 4: Pull from GitHub
 - Make a change to a file directly on GitHub (use the GitHub editor)
 - Pull that change to your local repo
 - Answer in your notes: What is the difference between git fetch and git pull?
 
## Created a new file "demo.txt" with some text on github repogitory under "DebOps_Demo.git"

## Created new empty directory on my system as "demo" to fork "DebOps_Demo.git" github repository.
# cd demo; ls -al
-bash: cd: demo: No such file or directory
total 8
drwxr-xr-x 2 root root 4096 Mar 14 11:30 .
drwxr-xr-x 5 root root 4096 Mar 14 03:19 ..

## git clone https://github.com/StarGithMd/DebOps_Demo.git
Cloning into 'DebOps_Demo'...
remote: Enumerating objects: 15, done.
remote: Counting objects: 100% (15/15), done.
remote: Compressing objects: 100% (7/7), done.
remote: Total 15 (delta 2), reused 12 (delta 2), pack-reused 0 (from 0)
Receiving objects: 100% (15/15), done.
Resolving deltas: 100% (2/2), done.

# ls -l
total 4
drwxr-xr-x 3 root root 4096 Mar 14 11:34 DebOps_Demo
# cd DebOps_Demo; ls -la
total 8
-rw-r--r-- 1 root root   21 Mar 14 11:34 demo.txt
-rw-r--r-- 1 root root 2351 Mar 14 11:34 git-commands.md

# cat demo.txt
This is the new file

## Task 5: Clone vs Fork
 - Clone any public repository from GitHub to your local machine
 - Fork the same repository on GitHub, then clone your fork
 - Answer in your notes:
 - What is the difference between clone and fork?
 - When would you clone vs fork?
 - After forking, how do you keep your fork in sync with the original repo?
 
## There are following difference between git fetch and git pull. 
 - git fetch: it help to Downloads commits, branches (git fetch origin, git log origin/main) and there is no make change in working files and remote-tracking.
 - git pull: it help to upload working file to remote repo and can make change (git fetch, git merge, git rebase) in file and configuration and sync brance to remote.
 
## When would you clone vs fork? 
 - Fork : Forking is best when require to create independent copy of a GitHub repository. Fork → Clone → Make changes → Push to fork → Pull request to original
 - Clone: Cloning is the best when required to work locally on code, test, and develop. Clone → Make changes → Push directly (if you have write access)
 
## After forking, how do you keep your fork in sync with the original repo?
 - To keep fork in sync with the original repository it need to add the upstream remote and regularly pull changes from it.
 - git remote add upstream https://github.com/StarGithMd/DebOps_Demo.git
 
