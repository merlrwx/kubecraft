Traceroute output showing the routing loop pattern:
```
docker exec clab-routing-basics-host1 traceroute -n -w 2 10.1.5.2
traceroute to 10.1.5.2 (10.1.5.2), 30 hops max, 60 byte packets
 1  10.1.1.1  0.525 ms  0.506 ms  0.499 ms
 2  10.1.2.2  0.851 ms  0.853 ms  0.855 ms
 3  10.1.2.1  0.473 ms  0.469 ms  0.463 ms
 4  10.1.2.2  0.829 ms  0.828 ms  0.825 ms
 5  * * *
 6  10.1.2.2  0.783 ms  0.399 ms  0.382 ms
 7  * * *
 8  10.1.2.2  1.231 ms * *
 9  * * *
10  * * *
11  * * *
12  10.1.2.2  1.930 ms  1.936 ms  1.936 ms
13  * * *
14  10.1.2.2  1.908 ms  1.909 ms  1.913 ms
15  * * *
16  10.1.2.2  1.892 ms  1.892 ms  1.889 ms
17  * * *
18  10.1.2.2  0.906 ms * *
19  * * *
20  * 10.1.2.2  2.419 ms  2.410 ms
21  * * *
22  10.1.2.2  2.390 ms  2.393 ms  2.398 ms
23  * * *
24  10.1.2.2  2.375 ms  2.376 ms  2.374 ms
25  * * *
26  10.1.2.2  1.951 ms  1.952 ms *
27  * * *
28  * * *
29  * * *
30  10.1.2.2  1.440 ms  1.443 ms  1.447 ms
```

TTL Explanation & How it prevents infinite loops:
TTL stands for Time To Live. In IP networking, TTL acts like a hop limit. Each router that forwards the packet decrements the TTL by 1. If the TTL reaches 0, the router drops the packet and usually sends an ICMP TTL exceeded message back.

In this exercise, the packet loops because srl1 sends traffic for 10.1.5.0/24 toward srl2, while srl2 sends traffic for 10.1.5.0/24 back toward srl1. The packet keeps bouncing between the two routers.

The packet eventually stops because the TTL reaches 0. This prevents the routing loop from continuing forever and consuming network resources indefinitely.

Traceroute shows the loop because it receives TTL exceeded replies from the routers. The repeated alternating hops between srl1 and srl2 show that the packet is stuck in a routing loop.


Simply put TTL is the packet’s maximum hop count. Every router reduces it by 1. When it hits 0, the packet is dropped. This stops routing loops from continuing forever.
