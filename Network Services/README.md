This would my first walkthrough so I will try to be as detailed as possible
Starting off with "Network Services"

#SMB

Understanding SMB
Questions 
1. What does SMB stand for ?
- "SMB - Server Message Block Protocol - is a client-server communication protocol used for sharing access to files, printers, serial ports and other resources on a network. [source]"

2. What type of protocol is SMB? - 
"The SMB protocol is known as a response-request protocol, meaning that it transmits multiple messages between the client and server to establish a connection."

3. What do clients connect to servers using?    
- TCP/IP
- "Clients connect to servers using TCP/IP (actually NetBIOS over TCP/IP as specified in RFC1001 and RFC1002), NetBEUI or IPX/SPX."
 
4. What systems does Samba run on?
 - "Samba, an open source server that supports the SMB protocol, was released for Unix systems."
 
 Enumerating SMB
 Questions
 1.  Conduct an nmap scan of your choosing, How many ports are open?
 After running nmap I found 3 ports opened
 
 
