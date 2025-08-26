
### CAPTURE RIPV@ ADVERTISEMENTS
```bash
tcpdump -i eth0 port 520 -vn
```
### CHANGE TTL
```bash
sudo sysctl -w net.ipv4.ip_default_ttl=NEW_TTL_VALUE
```
### Since you are dumb, here is a tunnel for mashing a reverse and connecting em
```bash
#Enable telnet with a tunnel. SSH on the 10.50.158.236 is using 7777.
IH$ ssh net1_student13@10.50.158.236 -p 7777 -L 11301:10.2.2.7:23 -NT
IH$ telnet 127.0.0.1 11301
#Now, we will create our reverse tunnel. We are utilizing the internal (.6) using it's ssh port. The 2222 states what our ssh port is to utilize for the function.
net1_comrade13$ ssh net1_student13@10.2.2.6 -p 7777 -R 11399:127.0.0.1:2222 -NT
#Next, create a local tunnel to bridge it. 
IH$ ssh net1_student13@10.50.158.236 -p 7777 -L 11302:127.0.0.1:11399 -NT
#Lastly,
IH$ ssh net1_comrade13@127.0.0.1 -p 11302 -D 9050 -NT
```
### THAT IS IT FOR A REVERSE TUNNEL IDIOT ^^^
###Capture SMTP Email
```bash
tcpdump -nn -l port 25 | grep -i 'MAIL FROM\|RCPT TO'
```
### Extract HTTP Passwords in POST Requests
bash```
tcpdump -s 0 -A -n -l | egrep -i "POST /|pwd=|passwd=|password=|Host:"
```
### Capture FTP Credentials and Commands
bash```
tcpdump -nn -v port ftp or ftp-data
```
### Capture all plaintext passwords
```bash
tcpdump port http or port ftp or port smtp or port imap or port pop3 or port telnet -l -A | egrep -i -B5 'pass=|pwd=|log=|login=|user=|username=|pw=|pas
```
