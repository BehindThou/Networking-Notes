### Bogurt
TCP dump 
to find IPv4 packets with at least dont fragment set: ip[6] & 0x40 = 0x40
Capture traffic with a source port higher than 1024 using correct transport layer headers: 'tcp[0:2] > 1024 || udp[0:2] > 1024'
Capture packets with UDP being set, utilizing ipv4 or ipv6: ip[9] = 0x11 || ip6[6] = 0x11
Capture packets in transport with only ACK/RST or ACK/FIN set: tcp[13] = 20 || tcp[13] = 17
Capture packets with IP ID Number field of 213: ip[4:2] = 213
Capture packets that contain a VLAN tag: ether[12:2] = 0x8100
Capture IPv4 packets with a DSCP value of 37: ip[1] >> 2 = 37
Capture all IPv4 packets targetting the begining of potential traceroutes (Can be windows or linux): ip[8] = 1 && ip[9] = 1 || ip[9] = 17 
Capture packets all DNS traffic: tcp[0:2] = 53 || tcp[2:2] == 53 || udp[0:2] = 53 || udp[2:2] = 53 
Capture packets looking for syn (Client attempting to connect): tcp[13] = 2
Capture packets looking for syn ack {Server responding to client): tcp[13] = 18
Capture packets looking for response packets from a server with closed tcp ports (RST): tcp[13] = 18
Capture TCP and UDP packets between well known ports: tcp[2:2] <= 1023 || udp[2:2] <= 1023
