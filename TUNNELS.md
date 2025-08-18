### TUNNELS TUNNELS TUNNELS TUNNELS
If ssh is messed up saying remote host identification has changed, use:
```bash
ssh-keygen -f "/home/student/.ssh/known_hosts" -R "172.16.82.106"
```
```bash
-L - Creates a port on the client mapped to a ip:port via the server

-D - Creates a port on the client and sets up a SOCKS4 proxy tunnel where the target ip:port is specified dynamically

-R - Creates the port on the server mapped to a ip:port via the client

-NT - Do not execute a remote command and disable pseudo-tty (will hang window)
```
```bash
Local Port Forwarding
ssh -p <optional alt port> <user>@<server ip> -L <local bind port>:<tgt ip>:<tgt port>

or

ssh -L <local bind port>:<tgt ip>:<tgt port> -p <alt port> <user>@<server ip>
Local Port Forward to localhost of server
Internet_Host:
ssh student@172.16.1.15 -L 1122:localhost:22
or
ssh -L 1122:localhost:22 student@172.16.1.15
Internet_Host:
ssh student@localhost -p 1122
Blue_DMZ_Host-1~$
```
```bash
Dynamic Port Forwarding
ssh <user>@<server ip> -p <alt port> -D <port> 2>/dev/null
or
ssh -D <port> -p <alt port> <user>@<server ip> 2>/dev/null
Proxychains default port is 9050

Creates a dynamic socks4 proxy that interacts alone, or with a previously established remote or local port forward.

Allows the use of scripts and other userspace programs through the tunnel.
```
```bash
ssh <user>@<server ip> -p <alt port> -D <port> 2>/dev/null
or
ssh -D <port> -p <alt port> <user>@<server ip> 2>/dev/null
```
### If given a box without knowing nothing else about box, utilize a Dynamic Port Forwarding 1 Step Tunnel
```bash
ssh student@172.16.1.15 -D 9050 2>/dev/null
```
### DO NOT PROXYCHAIN TELNET OR SSH
