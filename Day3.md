### Bogurt
TCP dump 
to find IPv4 packets with at least dont fragment set: ip[6] & 0x40 = 0x40
Capture traffic with a source port higher than 1024 using correct transport layer headers: 'tcp[0:2] > 1024 || udp[0:2] > 1024'

