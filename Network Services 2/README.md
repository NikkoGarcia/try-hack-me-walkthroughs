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
- 7

![Screen Shot 2021-02-04 at 6 56 33 AM](https://user-images.githubusercontent.com/55337670/106927326-22de3100-66b6-11eb-9632-21ade8dfce8e.png)
![Screen Shot 2021-02-04 at 6 57 31 AM](https://user-images.githubusercontent.com/55337670/106927459-44d7b380-66b6-11eb-8cfb-49836eb95f66.png)

2. Which port contains the service we're looking to enumerate?
- 2049

3. Now, use /usr/sbin/showmount -e [IP] to list the NFS shares, what is the name of the visible share?

![Screen Shot 2021-02-02 at 1 42 30 PM](https://user-images.githubusercontent.com/55337670/106677243-82282e00-655c-11eb-8489-8671654afffc.png)
- /home

5. Then, use the mount command we broke down earlier to mount the NFS share to your local machine. Change directory to where you mounted the share- what is the name of the folder inside?

![Screen Shot 2021-02-04 at 7 18 47 AM](https://user-images.githubusercontent.com/55337670/106930082-3b037f80-66b9-11eb-8007-395be21db3b1.png)
- cappucino

6. Interesting! Let's do a bit of research now, have a look through the folders. Which of these folders could contain keys that would give us remote access to the server?

![Screen Shot 2021-02-04 at 7 20 49 AM](https://user-images.githubusercontent.com/55337670/106930346-84ec6580-66b9-11eb-805c-dcbded42b6b6.png)
- .ssh

7. Which of these keys is most useful to us?

![Screen Shot 2021-02-04 at 7 21 52 AM](https://user-images.githubusercontent.com/55337670/106930464-a9484200-66b9-11eb-9ef9-b746927293bb.png)
- id_rsa
8. Can we log into the machine using ssh -i key-file username@ip ? (Y/N)
![Screen Shot 2021-02-04 at 7 24 29 AM](https://user-images.githubusercontent.com/55337670/106930798-080dbb80-66ba-11eb-84b5-9208eb5809c9.png)
- Y
