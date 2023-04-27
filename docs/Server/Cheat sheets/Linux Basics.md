# Linux cheat sheet

## basic
Do as root 
`sudo`

login as root  
`sudo bash`  

check running services
`systemctl --type=service --state=active`

basics
`whoami` 
`uname -a`
`lsb_release -a`
`hostnamectl`
`history` "shows history of used commands"
`man <command>` "shows manual for command"
`whatis <command>`
`echo <argument>`
`clear`
`alias <name>=<command>` "changes command"
`nano` "text editor"
`exit` and `logout`
`shutdown` , `halt` , `reboot` ,use with: `-h time "message"`, time can be absolute (hh:mm) or wait (+m)

package managers 
ubuntu `apt`
`apt-get`
`install`
`remove`
`remove --purge`
centOS and RHEL `yum` and `rpm`
ARCH `pacman`

Update upgrade  
```
sudo apt update && sudo apt upgrade -y
```  
  
## navigating folders 
`pwd` "destination to current location"
`ls` "files in current location"
- `-l` "list"
- `-la` "hidden files"
- `-lah` "show sizes in human-readable format"
`cd` "change directory"
`locate <filename>`  "shows path to filename
`find -name <filename or directory name>`  
`grep <search string> <filename>` "global regular expression print, search through text or file"

## file commands
`cat <filename>` "displays file content"
`file <filename>` "displays info about file"
`wc <filename>` "word count"
`touch <filename>` "modify existing file (or make new one)"
`cp <source file> <target file>` "copies file, provide path in `<target file>` to copy to target folder"
`mv <filename> ~/Directory/<filename>` "move files, also used for renaming"
`diff <file1> <file2>` "compares two files and prints difference"
`wget <url>` "downloading files from internet"
`curl` "alternative"

creating folders  
`mkdir <directory name>`
`rmdir <directory name>`  

`df` "disk free,shows available disk sapce, "
`du` "disk usage, shows how much file or directory takes, use `-h` for human readable format"
`head <filename` OR `<command> | head` "shows first 10 items in a file or command, `tail` last 10"

`tar` "compress comand, extract"

file permissions
`chmod <permission> <file or directory>`
`<permission>` used in three number format e.g. "777" , each numbers represents permission level of owner, group, everybody
- 0 **no permission**
- 1 e**x**ecute
- 2 **w**rite
- 4 **r**ead
- 5 6 7 combination of all above
`sudo chown <new owner name or UID> <file or directory>` "changes owner"

## processes
`ps` "process status"
`top` "table of processes"
`kill <signal option> <process ID>` "terminate process"
`<signal option>` "`-9` forces a stop, `-15` saves all progress", `<process ID>` found in top
check running services
```
systemctl --type=service --status=running
```

## user management
`sudo useradd <username>` "creates user"
`sudo userdel <username` "deletes user"
`passwd <user>` "alters password", no argument changes current user password