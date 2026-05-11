# Actions that you should be able to perform

## Create/Read/Update/Delete/Move files

- touch file.txt (To create files)
- cat file.txt (To read files)
- echo "Matter you want to add" >> file.txt (To update files, or you can use the vim command to write matter into that file)
- vim file.txt (In the editor, we will update the text file)
- rm file.txt (To remove empty file)
- rm -r file.txt (To remove non-empty files recursively)
- mv file.txt dir1/ (To move file.txt to inside dir1 directory)
- mv file.txt file1.txt (To rename files)
- cp file.txt copiedfile.txt (To copy a file into another file)


## Create/Read/Update/Delete/Move folders

- mkdir dir1 (To create a directory)
- cd dir1 (To change into dir1 directory)
- rmdir dir1 (To delete an empty directory)
- rm -r dir1 (To delete a non-empty directory)
- cp -r dir1 dir2 (To copy directory recursively)
- pwd (To display current directory)


## Check disk status
- df -h (To display disk status -h option helps to see details in a human-understandable language)
- du -sh (To check folder size -s for summary and -h for display in human-readable format)


## Check status of processes, able to extract process ids(hint: use pipe operator to combine ps, xargs and awk)
- ps -ef | awk '{print$2}' | xargs kill -9 (To kill the process using kill -9 to force kill, which came as a result of awk, which is to print the 2nd column, which gets the input from the output of ps -ef, which lists out all processes)


## Getting the most senior parent process
- firefox & (Start firefox)
- ps -ef | grep firefox (List the processes that are run by Firefox)
- ps -ef | grep firefox | grep -v grep | awk '{print$3}' (List out the parent PPIDs of processes run by Firefox)
- ps -fp 2358 (To trace the parent of 2358)
- ps -fp 2071  (To trace the parent of 2071 parent, Need to do this process until we get the senior-most parent process. Here, systemd is the most senior parent process)
```text
O/p:
UID         PID       PPID  C STIME TTY          TIME   CMD
sowmya      2071       1    0 14:04  ?        00:00:00 /usr/lib/systemd/systemd --user
```


## Change file permissions. Able to explain and manipulate the numerical file permissions. (chmod and chown)

- chmod 755 file.txt (7 for user/owner all rwx permissions, 5 for group read and execute, 5 for others read and execute. It will change the permissions of file.txt)
- chown sowmya:sowmya file.txt (It will change the ownership of file.txt for the owner, it will be sowmya, and for the group also it will be sowmya)
- chmod -R 755 file.txt (It will recursively change permissions of file.txt)


## Able to extract the last x lines from files, get word count for a particular word, and find a particular word. (Basics of sed or awk would do)
- tail -n 10 file.txt
- grep "Hello" file.txt | wc -l (To print the word count of " Hello " in the file.txt)
- grep "Hello" file.txt (It will show the lines that contain " Hello World. ")
- awk '{count += gsub(/Hello/,"")} END {print count}' file.txt (With awk, by using gsub(), it will check for a matching string and increase the count, and in the end it will print in the terminal)
- sed -n '/Hello/p' file.txt (-n option is to suppress default printing, and p option is to print the lines that consist of the Hello word)


## Basics of sed and awk
- sed is used mostly for the replacement and editing of text. Its full form is Stream Editor.
- Ex: sed 's/Linux/Ubuntu/' file.txt (s stands for substitute, it means in place of Linux substitute Ubuntu in file.txt)
      sed -n '2p' file.txt (-n to compress default printing and 2p will print two lines only in file.txt)
- awk is mostly used for processing and pattern-searching. If we give word structure to find out. It will do the process
- Ex: awk '{print $1}' data.txt (It will print the first column values in data.txt files)
      awk '/Kavya/' data.txt (Search for Kavya in the data.txt file)


## Difference between absolute and relative paths.
- Absolute path: It shows the path root '/'
- Relative path: It will depend on the current location. If I'm in file.txt in dir1. Then it will be like 'dir1/file.txt'  


## Learn how to use the find command
find command will help us to find out the things we need, like files, directories, hidden files, and text files. If we want to do manipulations on it or just to where it was.
- find . -name file.txt (To find the file.txt)
- find . -type f -name "*.txt" (To find out all .txt files. -name is case-sensitive and -type will tell the type of it, like whether it is a file or a directory or what)


## Learn ls with the 5 most commonly used flags used such as: -- View hidden files -- Sort by time -- Reverse sort -- Human readable file sizes -- Combining flags to get hidden files, sorted by time in reverse with human readable file sizes.
- ls -a (to see hidden files)
- ls -t (sort by time)
- ls -r (Reverse sort)
- ls -atrlh (Combines all flags to get hidden files, sorted by time in reverse with human-readable file sizes.


## Find out what are the terminal codes such as Ctrl+D, Ctrl+C, Ctrl+Z etc and use them
- Ctrl+D (To end input/logout) 
- Ctrl+C (To stop the process)
- Ctrl+Z (To suspend the process)
- Ctrl+L (To clear the terminal, and others will write a clear word)
- Ctrl+R (To reverse search)
- Ctrl+A (To go to the beginning of the file)
- Ctrl+E (To go to the end of the file)\


## Difference between Ctrl+C and Ctrl+Z
- Ctrl+C will help us to stop the process that we are doing. If we are pinging google.com, we can use this code to stop that process of pinging. It sends a signal of SIGINT 
- Ctrl+Z will help us to suspend the process. Sends SIGTSTP signal. To continue that process, we can use the fg or bg command.


## Find out how to use Ctrl+R to reverse search
It will help us to search the command history instantly, and we can reuse already used commands. It works faster, and there is no need to type 


## Find out how to use tab autocompletion
To use tab autocompletion, we can just write a few characters and press tab. If it understands what that file is and which is unique, it will print. But, up to those characters, there are so many files, which means we need to add some more characters to them.


## Find out how to use the arrow keys to navigate history
By pressing the up arrow key, we will go to the previous commands, and if we use the down arrow key, it will go to the commands, but if we are at the bottom and using the down arrow, it will not do anything.
And coming to the difference between these arrow keys and Ctrl+R is,
- By Ctrl+R, we will do search-based navigation by typing. But by the arrow, we need to keep pressing it until we reach our desired command to look into.






# Sample Review Questions

## Go into your home directory
cd ~

## Create a directory d1
mkdir d1

## Create a file a.txt inside it
touch d1/a.txt

## Check permission of a.txt. What are the permissions in decimal format
ls -l a.txt 
Permissions in decimal format is 664

## What are the three elements in the permission? Do you understand conversion of decimal to binary?
- Three elements in the permission for owner, group and others
- Yes, I understand the conversion of decimal to binary. For above a.txt the permission in binary will be - 110 110 100


## Change the permissions of a.txt to 755?
chmod 755 a.txt


## Add a directory d2
mkdir d2


## Add b.txt inside d2
touch d2/b.txt


## Change permissions of d2 (and everything inside to 755)
chmod -R 755 d2


## Start the firefox browser
firefox &


## List all processes in your computer
ps -ef


## Find pid of Firefox browser. Difference between parent process and child process(hint: you need to learn pipes)
ps -ef| grep firefox | grep -v grep | awk '{print$2}' 
- ps -ef will try to load all processes running in system
- grep firefox will only check for firefox
- grep -v grep will remove all the lines will come with the ouput of grep firefox process
- awk '{print$2}' will only print second column where PID's will be showed.


## Kill the process (Hint: pipes, awk, xargs, kill)
kill -9 2358 (Will kill the process with id 2358  -9 will tell to do the killing process forcefully


## What is your user in Linux?
My user in linux is sowmya. We can know it by giving whoami command.


## What is your group in Linux?
My group in linux is sowmya. We can check it by typing groups command.


## What is your computer architecture? (hint uname command, learn the flags)
- uname -m (Will help us to know our computer architecture. For me, it was x86_64)
- uname -a (To know all system info)
- uname -r (To about our kernel version. For me, it was 6.17.0-22-generic


## What is your audio driver? (hint: lspci, learn pipes and grep)
lspci | grep -i audio (lspci command will help us to have detailed information about PCI buses and hardware connected devices to the system. For me, the below output is shown)
0000:00:1f.3 Multimedia audio controller: Intel Corporation Raptor Lake-P/U/H cAVS (rev 01)


## Go to home folder. Use find command to find all occurrences of "java" text anywhere in any filename or directory name in your system?
cd ~
find . -name '*.java'


## List everything in the home directory to get all files (including hidden), sorted by time in reverse with human readable file sizes
ls -artlh


## Get last 30 lines for Harry Potter. Get word counts for particular words.
- tail -n 30 "Harry Potter.txt"
- grep -oi "Harry" "Harry Potter.txt" | wc -l




# Questions

## What is the difference between service and application?
- Service, is a background feature or program which helps to support the system or other applications to work.
- An application is a program directly used by the user. For example, Youtube, Swiggy, Flipkart etc.

## What are the wildcards ~,.,..,* and ?
- ~ represents for home directory
- . represents current working directory
- .. represents parent directory for current directory
- * used for matches anything
- ? matches only single character


## What are the different flags for kill? Why do we use kill -9 in general?
- -1 (to reload the process)
- -2 (to interrupt like Ctrl+C)
- -9 (to force kill)
- -15 (for graceful termination it will be used by default)
- -18 (continue stopped proces)
- -19 (to pause the process)

## Are you clear about file permissions? Explain them? chmod and chown commands?
Yes. Normally, we have three permissions.
- read(r) It gives the permission to read the file
- write(w) It gives the permission to write into the file
- execute(x) It gives permission to execute the file
chmod command will help us to modify the permissions
chown command will help us to change the ownerships of that file or directory

## Usage of Ctrl+R to search previously run commands, arrow keys, tab autocompletion.
- Ctrl+R will help us to reverse search the commands that we used previously. It was fast as as we use type some characters to get the entire command
- arrow keys will help us to go back to used commands in sequential order in reverse
It was fast as as we use type some characters to get the entire command
- arrow keys will help us to go back to used commands in sequential order in reverse
- tab autocompletion will help us to fill the commands easily by asking terminal to autofill by writing upto few characters to make it understand what it will be
- tab autocompletion will help us to fill the commands easily by asking terminal to autofill by writing upto few characters to make it understand what it will be

