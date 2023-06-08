## Files and Directory Notes

### Editing Files + Directories 
`$ touch filename.txt` creates a text file in the current working directory. To check which directory you are in enter `$ pwd`

`$ vim filename.txt` lets you create and edit the file at the same time 

`$ cat filename.txt` outputs contents of file in the terminal

You can also use `$ more filename.txt` which advances one screen at a time or `$ less filename.txt` which can be more consise if used with `$ less filename.txt | grep filter`

`$ cp file1 newfile2` duplicates a files contents to a new file. You can specify the path to a directory using `/dirname/dir/filename`

`$ mv filename /file/path/filename` can move files from one directory to another

`$ mkdir /dir/path/dirname` makes a new directory in specified location

`$ rm /path/to/dir/filename` removes the file from the specified directory

`$ rm -rf /path/to/dir` deletes a directory without warning 

`$ sudo find /dirname -name "filename"` searches for a file by name in your chosen directory

`$ sudo find /dirname -type f -name "*.type"` searches for all files ending with .type in your chosen directory. This can be .txt .log .html and more

`$ sudo find /dirname -type f -user username` searches for files in chosen directory owned by user username 

`$ scp -rp /dirname/dirname username@ip.addr:/dirname` sends a copy of directory from one server to another server with recursive r and preservative p

`$ rsync -aP /dirname/dirname username@ip.addrrp:/dirname` pushes a copy of directory from local onto another machine

### Using Multiple Machines

When you know the contents of second machine and would like to pull from a server you can use: 

`$ scp -rp username@ip.addr:/dirname /dirname/dirname` pulls a copy of directory from server to local machine recursive r and preservative p attr

`$ rsync -aP username@ip.addrrp:/dirname /dirname/dirname` pushes a copy of directory from server onto local machine 

### File Comparisons and Statistics  

`$ diff -c filename1 filename2` command contextually compares the two files line by line

`$ diff /dirname1 /dirname2` compars directories one and two for differences

`$ comm filename1 filename2` compares files in sorted order

`$ cmp filename1 filename2` simply returns the first difference it can find between files. Common to use for almost identical files

`$ stat filename` gives you information of the file including size, access date and read write permissions

`$ lsattr filename` lists the files attributes

`$ sudo chattr [-pRVf] filename` adds file attributes to filename with several optional 

### File and Directory Permissions 

`$ sudo su - username` allows you to log into machine as another user

`$ id username`allows you to view user permissions

Directory permissions take the form `drwxr-xr-x` and file permissions take the form `-rwxr-xr-x`

`$ ls -l` lists the contents of a directory including its file permissions with `ll -l` offering more information including hidden files

`$ sudo chown username filename ` changes the ownership of a filename to username

`$ sudo chown groupname:filename` changes the group ownership of a file to group

`$ sudo chmod 644 filename` changes file permissions numerically -  NOTE: most common numerical permissions are 777,  755,  644 and 660

`$ sudo chown -R usename1:groupname1 /home/deleteduser1` changing ownership recursively if assigning permissions to a deleted user

`$ sudo chown username:grpname` changes ownership of group

More complex problem solving can then be attained through layering commands together such as: 

`$ find /dirnam/appnam -name "d*" -ok chmod 660 {} \;` which finds an application name beginning with letter d, within specified directory, changes the permissions to 660 and asks for confirmation. 

`$ find /dirname -nouser -nogroup -exec chown username:grpname {} \;` finds files in directory not owned by any user OR any group and changes this to the specified user and group 

### Archiving Files 

`$ tar -cvzf archname.tar.gz /dir/filename` creates an archive of filename

`$ tar -tf archname.tar.gz` list what is in the archived files

`$ tar -tf myapp.tar.gz > app.list`redirects archive output into a file which can then be catted or filtered using grep

`$ ls -l /etc > etclist.txt` list out etc dir and output into file etclist but can be overwritten

`$ ls -l /etc >> etclist.txt` creates or appends file if already exists
