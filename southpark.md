### Hopefully got this mane
```bash
# I __ __ __. __, __ __ __ __ __ __ __
#Host eric, ssh is blocked for outsiders
IH$ telnet 10.50.151.62
#ip a reveals 192.168.100.33/27. cat /etc/ssh/sshd_config reveals 8462 is ssh. 
Eric$ ssh student@10.50.247.170 -R 21399:127.0.0.1:8462 -NT
#We need to bring it back with a local since ssh is disabled ssh Eric@127.0.0.1 -p 21300 -D 9050 -NT
IH$ ssh Eric@127.0.0.1 -p 21399 -L 21301:10.50.151.62:8462 -NT 
ssh Eric@127.0.0.1 -p 21399 -D 9050 -NT
#We are the .33. We are looking at Kenny, the 192.168.100.60
#Create the next tunnel
ssh Eric@127.0.0.1 -p 21399 -L 21302:192.168.100.60:22 -NT
ssh Kenny@127.0.0.1 -p 21302 -D 9050 -NT
#ip a reveals the 10.90.50.130/26. We will hunt the 10.90.50.140. .140 is kyle, he has an ssh port above the well known. (Port 6481)
ssh Kenny@127.0.0.1 -p 21302 -L 21303:10.90.50.140:6481 -NT (tunnel to kyle)
ssh Kyle@127.0.0.1 -p 21303 -D 9050 -NT
#172.20.21.4/28 is our next range, stan is the 172.20.21.5 and ssh to him is blocked
#We need to create a tunnel to be able to telnet
ssh Kyle@127.0.0.1 -p 21303 -L 21304:127.20.21.5:23 -NT
IH$ telnet 127.0.0.1 21304
#Create our reverse tunnel
Stan$ ssh Kyle@172.20.21.4 -p 6481 -R 21398:127.0.0.1:22 -NT (.4 is what stan sees kyle as, 6481 is kyles ssh.)

