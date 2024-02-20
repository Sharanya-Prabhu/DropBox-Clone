
# Dropbox Clone - A Files Backup Service

Inspired from real world applications like Google Drive and Dropbox, this project is a file hosting and storage service where users can upload, download, share, sync, and backup their files.
Different operating systems concepts such as multithreading, file system handling, distributed operating systems, symbolic links have been implemented for successful functioning of this service. The software is made compatible with multiple users as well as multiple systems using multithreading and distributed operating systems. Symbolic links are used to enable the user to share their files and resources with another user. This service is very helpful in a collaborative workspace as well as backing up of the user’s important files.


## Problem Statement

To provide a platform to backup files.
The real-world software Dropbox, is a platform providing three basic file management features to a user:
1) Upload and Download of files
2) Share files with another user
3) Synchronise files in the backup with those on his/her local system. 


Inspired from Dropbox, we aim to build a prototype that implements all of these basic features in a command line interface. 

## Methodology
By means of socket programming, we first establish a TCP connection between the user (the client) requesting connection and the always-ON server to enable reliable data transfer for our files. The server creates a new thread to service the client and goes back to listening for more connection requests. In the new thread, the user
is authenticated and presented with a menu of options to upload, download, delete, share and sync files from the server. Let’s look into each of these features in detail -

### User Authentication
To login to his/her account, the client/user is asked to enter the username and password to proceed further. These details are then
compared on the server side with the existing usernames and passwords in the database. If the correct username and password combination has been entered, the user is authorized and the server intimates the client to display a message accordingly. If the information entered is incorrect, the client is asked to try again.

### Upload

Firstly, on the client side, the user is asked to enter the filename of
the text file on his local system he wishes to upload to the server.
This information is sent to a function named textFileTransfer
wherein the file is opened and read character by character into a
string fileContents. This string and filename, along with the user
identification details is sent to the thread on the server side. The
server reads this information in the receiveFile function into a
structure object named info. The user identification information is
used to navigate to the user’s directory in the file system. A new
text file is created with the received file contents and saved in the
user’s directory with the name the same as that of the received filename.

### Download

In the download option, the client is asked to enter the filename of
the file he wishes to download from his backup at the server. After
the filename has been entered, it is immediately intimated to the
server, and it sends back to the client the file contents as a string.
A new file is created with the contents of the string that was received and saved with the same filename. The implementation of
Download is the opposite to that of Upload.

### Delete

In the delete option, the client will enter the name of the file on his
backup at the server that needs to be deleted. On the server side, in
the deleteFile function, the filename of the file to be deleted is read.
The correct path to the user’s file is obtained using the function
getPath. The C++ STL built-in function remove() deletes the file
on the server side.


### Share
For sharing, the user enters the username of the person he wants to
share a file with and the filename of the file that needs to be shared.
Symbolic Links, also known as symlinks, are file-system objects
that point toward another file or folder. These links act as shortcuts
with advanced properties that allow access to files from locations
other than their original place in the folder hierarchy by providing
operating systems with instructions on where the “target” file can
be found. On the server side, we create a symbolic link of the file
to be shared and place it in the receiver username’s directory. This
way the receiver can also access the same file from his own account. If the file has been successfully shared, the server sends a
file_status = 1 to the client. If the receiver’s username or the file to
be shared doesn’t exist, the server returns a file_status = 0 to the
client. The client displays a message accordingly.

### Display
The server sends one-by-one the names of all files residing in the
user’s directory in its database to the client. The client reads this
list of files and displays it to the user.

### Sync
To sync all the files in the user’s backup with the files on his local
system, a list of filenames in the user’s directory on the server side
is sent to the client. Every file from this list that exists on the client’s local system is re-uploaded to the server. This way on the
server’s side, the user’s files get overwritten and become up to date.





## Implementation

The concepts of Operating Systems make the very core of this project. This project is fully based on file system management wherein we create and maintain files and directories of users.
Multithreading is employed to create a new thread for every client such that multiple users can simultaneously use the file hosting service. Concepts of distributed operating systems is implemented so that multiple systems can access and work on this software. For efficient sharing of files symbolic links are used to create a shortcut to the owner’s file. User authentication is implemented to allow only authorized users to access their files. To avoid any possible deadlocks that may arise, semaphores are used.
In addition to that, hash maps are used for an effective user authentication and security. Lastly, socket programming is employed to establish a TCP connection between our server and the clients for reliable data transfer. These concepts are heavily implemented and integrated for smooth functioning of this service.
