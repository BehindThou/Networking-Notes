### finding specific hint
```bash
find . -name *3c*
```
### Change hex encrypted pcap to viewable pcap with xxd
```bash
xxd -r capstoneIam_HEX_ENCODED.pcap > glubnub.pcap
```
### Sneaky admin moved snort alerts.
```bash
ps -ef | grep snort
#Discovered /var/log/capstone through here.
```
### CAPTURE RIPV2 IP ADVERTISEMENTS
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
### Capture SMTP Email
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
Tables of iptables¶
filter - default table. Used to ACCEPT, DROP or REJECT packets that match. Provides packet filtering.

INPUT: packets going to the local machine
FORWARD: packets routed through the server
OUTPUT: locally generated packets
nat - used to translate private ↔ public address and ports.

PREROUTING: designating packets when they come in
POSTROUTING: locally generated packets before routing takes place
OUTPUT: altering packets on the way out
mangle - provides special packet alteration. Can modify various header fields.

PREROUTING: incoming packets
POSTROUTING: outgoing packets
INPUT: packets coming directly into the server
FORWARD: packets being routed through the server
OUTPUT: locally generated packets that are being altered
raw - used to configure exemptions from connection tracking.

PREROUTING: packets that arrive by the network interface
OUTPUT: processes that are locally generated
security - used for Mantator Access Control (MAC) networking rules.

INPUT: packets entering the server
FORWARD: packets passing through the server
OUTPUT: locally generated packets
