# Tunneling. Lets just hope that we figure this out soon

What tunnel should i make on the situation?

Does the Next device simply take another ssh coneection?
ssh student@Nextmachine -L 11411:127.0.0.1:22 <- port open on the next machine btw

and then to get in, 
ssh student@ 127.0.0.1 -p 11411

now how do you extend the basic tunnel. this should be it
ssh student@127.0.0.1 -p 11411 -L 11412:172.17.17.28:22 -NT
                                                      ^
                                                Port open on 172

# Dynamic Port Forwarding for Proxychains
This allows the using of commands on a foreien device. can be used to nmap, ./scan.sh. wget,
ssh student@ 127.0.0.1 -p 11411 -D 9050 -NT

# Remote Port Forwarding
Think of this as reaching BACKWARDS, grabbing a port and moving.
ssh username@backwards lookinging host ip (usually private) -R 11412:127.0.0.1:22

now back on the Internet Host
ssh username@forward facing of that same ip (usually public) -L 11413:127.0.0.1:11412 -NT
                                                                 ^                ^
                                                          On local machine     where its going to meet at

# Local Port forwarding to telnet into a machine
ssh user@public-ip -p 22 11415:172.17.17.20:23
telnet 127.0.0.1 11415






### REAL STUFF STARTS HERE
### METHOD TO THE MADNESS

# EXTERNAL RECON

```bash
./scan.sh
```
once you get what ports are open, do the following
```bash
wget -r ftp://ip.addres.goes.here
wget -r http://ip.address.goes.here
```

Now either you will need to telnet or SSH onto the remote machine. Depending on what it is do the following

# SSH
- SSH onto the device
- Internal Recon (netstat -antp, ip a)

exit and create tunnel
```bash
ssh user@ipaddress -L 11411:127.0.0.1:22 

#check it works, add -NT if it does.

#new terminal

ssh user@127.0.0.1 -p 11411 -D 9050 -NT

#new terminal for proxychains

proxychains ./scan.sh #get info
proxychains scp -p 11411 user@127.0.0.1:/usr/share/cctc/user-share.png /home/desktop

#check image for flag
```



# TELNET
- Telnet onto device (Telnet Ipaddress Port)
- Internal Recon (netstat -antp, ip a) (CHECK FOR SSH PORT 'cat /etc/ssh/sshd_config)
Create reverse tunnel
```bash
ssh student@10.50.247.183 -R 11411:127.0.0.1:RHP FOR SSH -NT

# new terminal

ssh user@127.0.0.1 -p 11411 -L 11412:ipaddress:RHP FOR SSH -NT

#new terminal

ssh user@127.0.0.1 -p 11411 -D 9050 -NT

#new terminal for proxychains

proxychains ./scan.sh #get info
proxychains scp -p 11411 user@127.0.0.1:/usr/share/cctc/user-share.png /home/desktop

#check image for flag
```
This is the process you will use for a majority of the test. IF there is no ssh port shown and no telnet, do a RHP scan on the foriegn IP for a ssh port. use that as the new ssh port from then on. 

```bash

#for example
IH>ssh bender@10.50.223.74 -p 1234 11412:172.17.17.28:23
IH>telnet 127.0.0.1 11412
 telnet Philip:password
#*now you can make a reverse tunnel. *
found that the ssh port was actually on 4321.
philip$ ssh previous-user@172.17.17.17 -p 1234 -R 11413:127.0.0.1:4321 #previous-user is to signify that the user is ONE step behind user philip$
#*new terminal, back on IH *
IH> ssh previous-user@10.50.223.74 -p 1234 -L 11414:127.0.0.1:11413 #previous-user is infront of the IH machine, several hops, however we make this tunnel to connect

#new terminal

ssh philip@127.0.0.1 -p 11414 # this brings you inside
ssh philip@127.0.0.1 -p 11414 -D 9050 -NT
#new terminal
proxychains :)

#its all a process. just need to find all potential ways of entry.
```
South Park made me have 10 different terminals open at once i want to die


## SCP a file back.
You will need a -D tunnel to that target and do the following
```bash
proxychains scp -p 11417 Stan@127.0.0.1:/usr/share/cctc/Stan-share.png /home/student
```
```bash
#this allows you to move files from the remote shares to your current working directory
scp -P 11417 Stan@127.0.0.1:/usr/share/cctc/Stan-share.png .
```


-p is the port the proxy chains is on. Stan is the user on the FOREIGN machine. and we are the /home student

proxychains nc 127.0.0.1 12345
