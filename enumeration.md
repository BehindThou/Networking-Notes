### PING ONE LINER
```bash
for i in {1..254}; do (ping -c 1 172.16.82.$i | grep "bytes from" &) ; done
```
TraceRoute Tool:
```bash
wget https://git.cybbh.space/cted/tech-college/cttsb/cctc/net/Net/-/raw/main/Resources/tr.py
```
Netcat Horizontal scan TCP for specific ports
```bash
for i in {1..254}; do nc -nvzw1 172.16.82.$i 20-23 80 2>&1 & done | grep -E 'succ|open'
```
Netcat Horizontal scan for UDP
```bash
for i in {1..254}; do nc -nuvzw1 172.16.82.$i 1000-2000 2>&1 & done | grep -E 'succ|open'
```
Netcat Vertical for TCP
```bash
nc -nzvw1 172.16.82.106 21-23 80 2>&1 | grep -E 'succ|open'
```
for UDP
```bash
nc -nuzvw1 172.16.82.106 1000-2000 2>&1 | grep -E 'succ|open'
```
Netcat TCP scan
```bash
#!/bin/bash
echo "Enter network address (e.g. 192.168.0): "
read net
echo "Enter starting host range (e.g. 1): "
read start
echo "Enter ending host range (e.g. 254): "
read end
echo "Enter ports space-delimited (e.g. 21-23 80): "
read ports
for ((i=$start; i<=$end; i++))
do
    nc -nvzw1 $net.$i $ports 2>&1 | grep -E 'succ|open' &
done
wait
```
Netcat UDP scan
```bash
#!/bin/bash
echo "Enter network address (e.g. 192.168.0): "
read net
echo "Enter starting host range (e.g. 1): "
read start
echo "Enter ending host range (e.g. 254): "
read end
echo "Enter ports space-delimited (e.g. 21-23 80): "
read ports
for ((i=$start; i<=$end; i++))
do
    nc -nuvzw1 $net.$i $ports 2>&1 | grep -E 'succ|open' &
done
wait
Netcat - Banner Grabbing
Find what is running on a particular port

nc [Target IP] [Target Port]
nc 172.16.82.106 22
nc -u 172.16.82.106 53
-u : To switch to UDP

Curl and Wget
Curl - Displays ASCII

curl http://172.16.82.106
curl http://172.16.82.106 -o output.txt
curl ftp://172.16.82.106
curl ftp://172.16.82.106 -u student:password
curl ftp://172.16.82.106/file.txt -o output.txt
Describe Methods Used for Passive Internal Discovery
recon3
Packet Sniffers
Wireshark

Tcpdump

p0f

Limited to traffic in same local area of the network

Describe Methods Used for Active Internal Discovery
recon4
```
Netcat Banner Grabbing (What is running on a specific port?)
```bash
nc [Target IP] [Target Port]
nc 172.16.82.106 22
nc -u 172.16.82.106 53
(-u = UDP)
```
