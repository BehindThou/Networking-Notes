### Idek anymore man.
```bash
IH$ telnet 10.50.87.199
Rick$ ssh student@10.50.247.170 (THIS IS MY FLOAT IP) -R 1111:127.0.0.1:22
IH$ ssh Rick@127.0.0.1 -p 4646

IH$ ssh Rick@localhost -p 1111 -L 2222:10.1.2.18:2222
IH$ ssh Morty@localhost -p 2222 -L 3333:172.16.10.121:2323
IH$ ssh Jerry@127.0.0.1 -p 3333 -L 4444:192.168.10.69:22
