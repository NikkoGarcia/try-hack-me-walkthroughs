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

Task 4 Exploiting NFS
1. Now, we're going to add the SUID bit permission to the bash executable we just copied to the share using "sudo chmod +[permission] bash". What letter do we use to set the SUID bit set using chmod?

![Screen Shot 2021-02-04 at 5 18 27 PM](https://user-images.githubusercontent.com/55337670/106985158-015c6400-670d-11eb-81a3-96108419bf78.png)
- sudo chmod +S bash

2. Let's do a sanity check, let's check the permissions of the "bash" executable using "ls -la bash". What does the permission set look like? Make sure that it ends with -sr-x.
- -rwsr-sr-x

3. Find the root flag

![Screen Shot 2021-02-04 at 5 20 43 PM](https://user-images.githubusercontent.com/55337670/106985325-5304ee80-670d-11eb-94e3-89acaef950ee.png)

Task 5 Understanding SMTP
Questions
1. What does SMTP stand for?
- Simple Mail Transer Protocol

2. What does SMTP handle the sending of?
- emails

3. What is the first step in the SMTP process?
- SMTP Handshake

4.  What is the default SMTP port?
- 25

5. Where does the SMTP server send the email if the recipient's server is not available?
- smtp queue

6.  On what server does the Email ultimately end up on?
- POP/IMAP

7. Can a Linux machine run an SMTP server? (Y/N)
- Y

8. Can a Windows machine run an SMTP server? (Y/N)
- Y

Task 6 Enumerating SMTP
Questions 
1. First, lets run a port scan against the target machine, same as last time. What port is SMTP running on?

![Screen Shot 2021-02-08 at 9 28 13 AM](https://user-images.githubusercontent.com/55337670/107271197-f9900e80-69ef-11eb-9f85-f5ae713e4270.png)
- 25

2. Okay, now we know what port we should be targeting, let's start up Metasploit. What command do we use to do this? 
- msfconsole

3.  Let's search for the module "smtp_version", what's it's full module name? 

![Screen Shot 2021-02-05 at 5 32 06 PM](https://user-images.githubusercontent.com/55337670/107400999-83021800-6aa6-11eb-853c-63f9eb3c35fa.png)

- auxiliary/scanner/smtp/smtp_version

4. Great, now- select the module and list the options. How do we do this?

![Screen Shot 2021-02-05 at 5 33 04 PM](https://user-images.githubusercontent.com/55337670/107401503-09b6f500-6aa7-11eb-9f5c-259a26b4649d.png)

- options

5. Have a look through the options, does everything seem correct? What is the option we need to set?

![Screen Shot 2021-02-05 at 5 36 25 PM](https://user-images.githubusercontent.com/55337670/107401605-23f0d300-6aa7-11eb-9381-2b73770a6a52.png)

- rhost

6. Set that to the correct value for your target machine. Then run the exploit. What's the system mail name?

![Screen Shot 2021-02-05 at 5 38 32 PM](https://user-images.githubusercontent.com/55337670/107401863-61edf700-6aa7-11eb-8505-0fe579322716.png)

- polosmtp.home

7. What Mail Transfer Agent (MTA) is running the SMTP server? This will require some external research.
- Postfix

8.  Good! We've now got a good amount of information on the target system to move onto the next stage. Let's search for the module "smtp_enum", what's it's full module name? 

![Screen Shot 2021-02-05 at 5 39 19 PM](https://user-images.githubusercontent.com/55337670/107402358-f22c3c00-6aa7-11eb-9914-f818c2f048a6.png)

- auxiliary/scanner/smtp/smtp_enum

9. What option do we need to set to the wordlist's path?

![Screen Shot 2021-02-05 at 5 42 02 PM](https://user-images.githubusercontent.com/55337670/107402635-49321100-6aa8-11eb-9ed9-38c2d7127bc3.png)

-USER_FILE

10. Once we've set this option, what is the other essential paramater we need to set?

![Screen Shot 2021-02-05 at 5 46 32 PM](https://user-images.githubusercontent.com/55337670/107402805-7b437300-6aa8-11eb-9ed8-451295b9d2ad.png)

- RHOSTs

11. Okay! Now that's finished, what username is returned?

![Screen Shot 2021-02-05 at 5 59 28 PM](https://user-images.githubusercontent.com/55337670/107402903-944c2400-6aa8-11eb-9bf4-b9fe9dda1d70.png)

- administrator

Task 7 Exploiting SMTP
Questions

1. What is the password of the user we found during our enumeration stage?

![Screen Shot 2021-02-09 at 8 52 26 AM](https://user-images.githubusercontent.com/55337670/107460845-f6367900-6afc-11eb-871a-917b6d3f8b9c.png)

![Screen Shot 2021-02-09 at 8 51 49 AM](https://user-images.githubusercontent.com/55337670/107460877-051d2b80-6afd-11eb-96fd-626a35c613a2.png)

-alejandro

2.Great! Now, let's SSH into the server as the user, what is contents of smtp.txt

![Screen Shot 2021-02-09 at 8 52 55 AM](https://user-images.githubusercontent.com/55337670/107460987-372e8d80-6afd-11eb-81e0-0d66c400acc6.png)
