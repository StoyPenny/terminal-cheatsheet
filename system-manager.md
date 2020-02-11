# System Management

This is a quick reference guide to common terminal commands that are used for managing your system.

---------------
<br><br>

### Show Realtime Processes
Show the realtime processses that are currently running processes on the system. 
```cmd
top   // Show realtime processes, memory usage, and CPU usage
q     // Quit the TOP command
```
<br>

### Show System Details
Similar to the top command, this command shows high level system details along with the memory. 
```cmd
htop   // Show a different view of all currently running processses on the system
q      // Quit the HTOP command
```
<br>

### Show Memory Usage
Show the system's memory usage.
```cmd
free -m
```
<br>

### Kill Process by ID
Enter the process id after the following command to kill that process.
```cmd
kill pid
```
<br>

### Kill Process by Name
Enter the process name after the following command to kill that process.
```cmd
pkill name
```
<br>

### Disk Usage
Running this will show the space usage of each folder in the current directory. Add the -h to the command to make it human readable. Adding the -s prevents recursiveness and shows the total size of a folder. The asterisk gets all the files and directories inside the current directory. 
```cmd
du -sh *
```
<br>

### Get Hardware Information
Get system hardware information such as Memory, CPU, disks, etc.
```cmd
sudo lshw // Full detailed view
lshw -short // Short detail view
```
<br>

### Get CPU Information 
Get detailed information about the CPU on your machine
```cmd
lscpu
```
