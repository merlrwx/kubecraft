1.
```text
❯ docker exec clab-ip-fundamentals-host1 ip addr show eth1
9: eth1@if10: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 9500 qdisc noqueue state UP
    link/ether aa:c1:ab:b7:68:e0 brd ff:ff:ff:ff:ff:ff
    inet 10.1.1.200/30 scope global eth1
       valid_lft forever preferred_lft forever
    inet6 fe80::a8c1:abff:feb7:68e0/64 scope link
       valid_lft forever preferred_lft forever
```


2. Calculate the /30 subnet for 10.1.1.200:
Network:    10.1.1.200
Usable:     10.1.1.201 - 10.1.1.202
Broadcast:  10.1.1.203


3. Is srl1 (10.1.1.1) within that range? Why or why not?
10.1.1.1 is NOT inside 10.1.1.200 - 10.1.1.203
Therefore srl1 is not on the same subnet as 10.1.1.200/30.

4.
```
docker exec clab-ip-fundamentals-host1 ip addr del 10.1.1.200/30 dev eth1
docker exec clab-ip-fundamentals-host1 ip addr add 10.1.1.2/24 dev eth1
```

5.
```
❯ docker exec clab-ip-fundamentals-host1 ping -c 3 10.1.1.1
PING 10.1.1.1 (10.1.1.1): 56 data bytes
64 bytes from 10.1.1.1: seq=0 ttl=64 time=3.615 ms
64 bytes from 10.1.1.1: seq=1 ttl=64 time=1.625 ms
64 bytes from 10.1.1.1: seq=2 ttl=64 time=1.634 ms

--- 10.1.1.1 ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 1.625/2.291/3.615 ms
```
