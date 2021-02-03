Task 2 - Understanding NFS

Questions
1. What does NFS stand for?
- Network File System
2.  What process allows an NFS client to interact with a remote directory as though it was a physical device?
- Mounting
3.  What does NFS use to represent files and directories on the server?
- File Handle
4. What protocol does NFS use to communicate between the server and client?
- RPC
5. What two pieces of user data does the NFS server take as parameters for controlling user permissions? Format: parameter 1 / parameter 2
- user id / group id
6. Can a Windows NFS server share files with a Linux client? (Y/N)
- Y
7. Can a Linux NFS server share files with a MacOS client? (Y/N)
- Y
8. What is the latest version of NFS? [released in 2016, but is still up to date as of 2020] This will require external research.
- 4.2

Task 3 - Enumerating NFS
Questions
1. Conduct a thorough port scan scan of your choosing, how many ports are open?
2. Which port contains the service we're looking to enumerate?
3. Now, use /usr/sbin/showmount -e [IP] to list the NFS shares, what is the name of the visible share?

![Screen Shot 2021-02-02 at 1 42 30 PM](https://user-images.githubusercontent.com/55337670/106677243-82282e00-655c-11eb-8489-8671654afffc.png)

4.  Change directory to where you mounted the share- what is the name of the folder inside?
5.Have a look inside this directory, look at the files. Looks like  we're inside a user's home directory...
6. Interesting! Let's do a bit of research now, have a look through the folders. Which of these folders could contain keys that would give us remote access to the server?
7. Which of these keys is most useful to us?
8. Can we log into the machine using ssh -i key-file username@ip ? (Y/N)
