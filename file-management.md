# File Management

A collection of useful terminal commands that will enable you to more effectively manage the files on your machine or server. 

---------------
<br><br>

### Change Directory
Change the currently active directory in the command line. 
```cmd
cd /directory/name/   // Go to a specific directory
cd ..                 // Go up a directory
```
<br>

### List Files / Folders 
Show a list of files and folders in the current directory. Add the -l flag to show the file permissions and owners alongside the other details. 
```cmd
ls       // List all of the files and directories in the currenly active directory
ls -l    // List all of the files and directories alongside of their owner:group and file permission information
ls -a    // List all of the files and directories, including hidden files
dir      // Show a list of files and folders in the current directory
tree     // Show a hierarchy a folders and files from the current directory
```
<br>

### Make A Directory
Use the following command to create a directory. 
```cmd
mkdir /my-directory/
```
<br>

### Create A File
Create a single blank file with the following command
```cmd
touch file.name
```
<br>

### Copy A File or Directory
Create a copy of a file or directory with the following command. 
```cmd
cp original.file copy.file 
```
<br>

### Move A File or Directory
Move a file or directory with the following command. 
```cmd
mv file.name /new/location/file.name 
```
<br>

### Remove A File
Remove a file or directory from the system. To recursively delete items in a directory, add the -R flag to the command. 
```cmd
rm file.name
```
<br>

### Remove A Directory
Remove a directory and all sub directories by using the rm command with the -R flag to recursively remove all files and folders within the specified directory. 
```cmd
rm -R /path/to/be/deleted/
```
<br>

### Change File Permissions
Use the following command to change the file permissions for a single file. To make this work recursively in a directory, add the -R flag before specifying the folder. 
```cmd
chmod 775 file.name
```
<br>

### Change File Owner
Change the file owner and group with the following command. To make this work recursively in a directory, add the -R flag before specifying the folder.
```cmd
chown user:group file.name
```
<br>

### Archive Files / Directories
Archive multiple files and directories together. 
```cmd
tar -cf archive.tar file1 file2 file3
```
<br>

### Unarchive Files / Directories
Extract files from an archive
```cmd
tar -xf archive.tar
```
<br>

### Create Compressed Archive
Create a compressed gzipped archive. 
```cmd 
tar -czf file.tar.gz inputfile1 inputfile2
```
<br>

### Extract Compressed Archive
Uncompress a gzipped archive.
```cmd
tar -xzf file.tar.gz
