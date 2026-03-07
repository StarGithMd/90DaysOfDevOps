## Day 06– Linux Fundamentals: Read and Write Text Files
- Today’s goal is to practice basic file read/write using only fundamental commands.

## Create a new file "notes.txt" and write text into it.

# touch notes.txt
# echo "Line 1" > notes.txt
# echo "Line 2" >> notes.txt
# echo "Line 3" | tee -a notes.txt
Line 3

# cat notes.txt
Line 1
Line 2
Line 3

# head -n 2 notes.txt
Line 1
Line 2

# tail -n 2 notes.txt
Line 2
Line 3

# echo "Hello, Linux world!" > myfile.txt; ls -l 
-rw-r--r-- 1 root root   20 Mar  7 09:40 myfile.txt

# cat myfile.txt
Hello, Linux world!

# echo "This is another line." >> myfile.txt
# cat myfile.txt
Hello, Linux world!
This is another line.

# tail myfile.txt		>> View 10 line from last of file.
Hello, Linux world!
This is another line.

# head myfile.txt	>> View 10 line from top of file.
Hello, Linux world!
This is another line.

# grep "Hello" myfile.txt	>> Search the file contents.
Hello, Linux world!

# ls -l myfile.txt
-rw-r--r-- 1 root root 42 Mar  7 09:43 myfile.txt

# vi myfile.txt 			>> Created new file and edited some text into it
# cat myfile.txt
This is the second file
added into new lines
