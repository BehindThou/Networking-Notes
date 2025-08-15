### PING ONE LINER
```bash
for i in {1..254}; do (ping -c 1 172.16.82.$i | grep "bytes from" &) ; done
