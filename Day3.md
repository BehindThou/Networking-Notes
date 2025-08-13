### Bogurt
TCP dump 
to find IPv4 packets with at least dont fragment set: ip[6] & 0x40 = 0x40
Capture traffic with a source port higher than 1024 using correct transport layer headers: 'tcp[0:2] > 1024 || udp[0:2] > 1024'
Capture packets with UDP being set, utilizing ipv4 or ipv6: ip[9] = 0x11 || ip6[6] = 0x11
Capture packets in transport with only ACK/RST or ACK/FIN set: tcp[13] = 20 || tcp[13] = 17
Capture packets with IP ID Number field of 213: ip[4:2] = 213
Capture packets that contain a VLAN tag: ether[12:2] = 0x8100
