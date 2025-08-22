IH$ ssh Sterling@10.50.93.47 -L 21301:127.0.0.1:22 -NT
IH$ scp Sterling@10.50.93.47:/usr/share/cctc/Sterling-share.png
IH$ ssh Sterling127.0.0.1 -p 21301 -L 21302:10.1.2.200:23 -NT
IH$ telnet 127.0.0.1 21302
Lana$ ssh Sterling@10.1.2.130 -R 21399:127.0.0.1:8976 -NT
IH$ ssh Sterling@127.0.0.1 -p 21301 -L 21303:127.0.0.1:21399
IH$ ssh Lana@127.0.0.1 -p 21303 -D 9050 -NT
$IH ip a


IH$ ssh sterling@10.50.93.47 -L 1111:10.1.2.200:23
IH$ telnet localhost 1111
Lana$ ssh Sterling@10.1.2.130 -R 2222:Localhost:8976
IH$ ssh Sterling@10.50.93.47 -L 3333:localhost:2222
IH$ ssh Lana@localhost -p 3333 -L 4444:10.2.5.20:22
IH$ ssh Cheryl@localhost -p 4444 -L 5555:10.3.9.39:23 
IH$ telnet localhost 5555
Malory$ ssh Cheryl@10.3.9.33 -R 6666:localhost:3597
IH$ ssh Cheryl@localhost -p 4444 -L 7777:localhost:6666
IH$ ssh Malory@localhost -p 7777 -D 9050
IH$ [rpxucjaoms mc ;pca;jpst 58246

