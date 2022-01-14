# Lab Report 1 Week 2
This lab report functions as a tutorial for completing CSE 15L Lab 1.  
The following steps will be covered:
 - Installing VS Ccode
 - Remotely Connecting
 - Trying Some Commands
 - Moving Files with `scp`
 - Setting an SSH Key
 - Optimizing Remote Running 

## Installing VS Code
Doing this consists of visiting [code.visualstudio.com](https://code.visualstudio.com/) and following the instructions to download and install it on your device. Once it is installed and you open VS Code, you should see a window that looks like this:
![VS Code](vscodewindow.png)

## Remotely Connecting
The first step to connecting to your course-specific account for 15L if you are using Windows is to [install OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse). Make sure you run PowerShell as an Administrator for the commands to work correctly. To setup your course-specific account, visit [sdacs.ucsd.edu/~icc](https://sdacs.ucsd.edu/~icc/index.php) and set your password. Your username will start with `cs15lwi22` followed by three letters unique to your account. To connect to the remote server, run this command in any terminal, with the `###` replaced by your unique letters: `ssh cs15lwi22###@ieng6.ucsd.edu`  
You can open a terminal in VS Code with Ctrl+\` or CMD+`, or by using Terminal > New Terminal in the menu. After entering your password, you should see something like this:
```
PS C:\Users\chuck\Documents\GitHub\cse15l-lab-reports> ssh cs15lwi22alj@ieng6.ucsd.edu
Password: 
Last login: Fri Jan 14 09:28:05 2022 from c-01-234-56-789.hsd1.ca.comcast.net
quota: No filesystem specified.
Hello cs15lwi22alj, you are currently logged into ieng6-203.ucsd.edu

You are using 0% CPU on this system

Cluster Status
Hostname     Time    #Users  Load  Averages
ieng6-201   09:30:01   15  2.06,  2.19,  2.21
ieng6-202   09:30:01   8   2.15,  2.13,  2.09
ieng6-203   09:30:01   7   2.24,  2.28,  2.23


Fri Jan 14, 2022  9:31am - Prepping cs15lwi22
[cs15lwi22alj@ieng6-203]:~:33$
```
You are now connected to the remote server through SSH, and any commands you run here will run on the remote server.

## Trying Some Commands
Run the command `pwd`. This prints the working directory, meaning the directory you are currently in. You can change directory using `cd [dir]`. Replacing `[dir]` with a directory will move you into that directory. The `ls` command will list the contents of the current directory. Putting `man` before a command will bring up a manual describing the command and its arguments. Run `man ls` and read what some of the arguments do, then try running `ls` with some of those arguments. For example, `ls -oat` will list all files sorted by date last modified.
```
[cs15lwi22alj@ieng6-203]:~:72$ ls -oat
total 136
-rw-r--r--   1 cs15lwi22alj  1327 Jan 14 09:31 .modulesbegenv
-rw-------   1 cs15lwi22alj   316 Jan 14 09:28 .bash_history
drwxr-s---   2 cs15lwi22alj  4096 Jan 14 09:27 .ssh
-rw-r-----   1 cs15lwi22alj     0 Jan 14 09:13 .motd
drwxr-sr-x 634 cs15lwi22    49152 Jan 12 08:05 ..
-rw-------   1 cs15lwi22alj     0 Jan  5 17:56 .history
-rw-r-----   1 cs15lwi22alj   574 Jan  5 17:50 WhereAmI.class
-rw-r--r--   1 cs15lwi22alj   318 Jan  5 17:50 WhereAmI.java
drwxr-s---   7 cs15lwi22alj  4096 Jan  5 17:00 .
drwxr-sr-x   3 cs15lwi22alj  4096 Jan  3 10:16 .cache
drwxr-sr-x   2 cs15lwi22alj  4096 Jan  3 10:16 perl5
drwxr-sr-x   3 cs15lwi22alj  4096 Jan  3 10:16 .local
drwxr-sr-x   3 cs15lwi22alj  4096 Jan  3 10:16 .config
-rwxr-x---   1 cs15lwi22alj   290 Dec 20 13:37 .zshrc
-rwxr-x---   1 cs15lwi22alj   481 Dec 20 13:37 .zshenv
-rwxr-x---   1 cs15lwi22alj  1931 Dec 20 13:37 .zprofile
-rwxr-x---   1 cs15lwi22alj  1961 Dec 20 13:37 .profile
-rwxr-x---   1 cs15lwi22alj   837 Dec 20 13:37 .procmailrc
-rwxr-x---   1 cs15lwi22alj   431 Dec 20 13:37 .login
-rwxr-x---   1 cs15lwi22alj   155 Dec 20 13:37 .locallogin
-rwxr-x---   1 cs15lwi22alj  1692 Dec 20 13:37 .kshrc
-rwxr-x---   1 cs15lwi22alj  1931 Dec 20 13:37 .cshrc
-rwxr-x---   1 cs15lwi22alj  1721 Dec 20 13:37 .bashrc
-rwxr-x---   1 cs15lwi22alj   975 Dec 20 13:37 .bash_profile
[cs15lwi22alj@ieng6-203]:~:73$
```
Running `cat` with a filepath with print the contents of that file. Use `exit`, `logout`, or Ctrl+D to disconnect from the remote server.

## Moving Files with `scp`
You can copy files from your client to the remote server using the `scp` command. For example, running  
`scp vscodewindow.png cs15lwi22alj@ieng6.ucsd.edu:~/`  
and entering your password will copy the `vscodewindow.png` file from the current directory on your client to the home directory ( `~/` ) on the remote server. Running `ssh cs15lwi22alj@ieng6.ucsd.edu "ls"` will list the contents of the home directory on the remote server, and should confirm that the file transfer was successful.
```
PS C:\Users\chuck\Documents\GitHub\cse15l-lab-reports> ssh cs15lwi22alj@ieng6.ucsd.edu "ls -ot"
Password: 
total 44
-rw-r--r-- 1 cs15lwi22alj 27028 Jan 14 10:08 vscodewindow.png
-rw-r----- 1 cs15lwi22alj   574 Jan  5 17:50 WhereAmI.class
-rw-r--r-- 1 cs15lwi22alj   318 Jan  5 17:50 WhereAmI.java
drwxr-sr-x 2 cs15lwi22alj  4096 Jan  3 10:16 perl5
```
As shown in the directory above, files like `WhereAmI.java` can be copied to the remove server. You can compile and run this program remotely by running `javac WhereAmI.java` and `java WhereAmI` on the remote server.
```
[cs15lwi22alj@ieng6-203]:~:90$ javac WhereAmI.java
[cs15lwi22alj@ieng6-203]:~:91$ java WhereAmI
Linux
cs15lwi22alj
/home/linux/ieng6/cs15lwi22/cs15lwi22alj
/home/linux/ieng6/cs15lwi22/cs15lwi22alj
```

## Setting an SSH Key

## Optimizing Remote Running