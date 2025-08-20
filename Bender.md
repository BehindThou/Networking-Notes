### Im starting to know man
```bash
#We know Bender is running ssh on a rhp. We did this:
 nc 10.50.223.74 1234
#This told us 1234 is running ssh. We will now create our tunnel
ssh Bender@10.50.223.74 -p 1234 (This is because we must specify since ssh is running on 1234) -L 21301:127.0.0.1:22
#Now we must create a DYNAMIC tunnel to scan the net 172.17.17/28 that we discovered)
ssh Bender@10.50.223.74 -p 1234 -D 9050 -NT (We must always create dynamic Tunnels to the server ip, and specify -p with the port being used from earlier)
#We have completed scans, acquired info, and discovered Phillip is the 172.17.17.28. OUR FACING IP IS 172.17.17.17 We have also discovered ssh is closed to outsiders. TELNET IS OPEN*
#We will use PROXYCHAINS AND OUR DYNAMIC TUNNEL to telnet into Philip
#Do recon, we have discovered the 192.168.30.130/26.
#We also discovered the 4321 port, but since we are in telnet, we cannot nc it normally. instead, we can cat /etc/ssh/sshd_config
#wE WILL NOW CREATE OUR REVERSE TUNNEL TO BENDER
ssh Bender@172.17.17.17 -p 1234 -R 21399:127.0.0.1:4321 -NT (-p 1234 is ssh running on Bender, 4321 is the ssh we discovered Philip)

IH$ ssh Bender@10.50.223.74 -p 1234
IH$ ssh Bender@10.50.223.74 -p 1234 -D 9050 -NT
Bender$ telnet 172.17.17.28
IH$ ssh Bender@10.50.223.74 -p 1234 -L 1111:172.17.17.28:23
IH$ telnet localhost 1111
philip$ ssh Bender@172.17.17.17 -p 1234 -R 21399:127.0.0.1:4321 -NT
IH$ ssh Bender@10.50.223.74 -p 1234 -L 21302:127.0.0.1:21399 -NT
IH$ ssh Philip@127.0.0.1 -p 21399 -D 9050 -NT
IH$ ssh Philip@127.0.0.1 -p 21302 -L 21303:192.168.30.150:1212
IH$ ssh Philip@127.0.0.1 -p 21303 -L 21304:10.10.12.121:2932
IH$ ssh proffesor@127.0.0.1 -p 21304 -D 9050 -nt
IH$ proxychains nc 127.0.0.1 23456
