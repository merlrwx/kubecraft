1. Pings

Success:
docker exec clab-ip-fundamentals-host1 ping -c 3 10.1.1.1
docker exec clab-ip-fundamentals-host2 ping -c 3 10.1.3.1
Inside SR Linux: ping 10.1.2.2 network-instance default

Fail:
docker exec clab-ip-fundamentals-host1 ping -c 3 10.1.3.2


2. ARP Table Entries

```text
host1
? (172.20.20.1) at 16:f9:f7:14:35:5a [ether]  on eth0
? (10.1.1.1) at 1a:d0:02:ff:00:01 [ether]  on eth1
```


```text
srl1
+------+------+--------------+------+----------+-------------------+
| Inte | Subi |   Neighbor   | Orig |   Link   |      Expiry       |
| rfac | nter |              |  in  |  layer   |                   |
|  e   | face |              |      | address  |                   |
+======+======+==============+======+==========+===================+
| ethe |    0 |     10.1.1.2 | dyna | AA:C1:AB | 3 hours from now  |
| rnet |      |              |  mic | :B7:68:E |                   |
| -1/1 |      |              |      | 0        |                   |
| ethe |    0 |     10.1.2.2 | dyna | 1A:7B:03 | 3 hours from now  |
| rnet |      |              |  mic | :FF:00:0 |                   |
| -1/2 |      |              |      | 1        |                   |
| mgmt |    0 |  172.20.20.1 | dyna | 16:F9:F7 | 3 hours from now  |
| 0    |      |              |  mic | :14:35:5 |                   |
|      |      |              |      | A        |                   |
+------+------+--------------+------+----------+-------------------+
```


3. Cross-subnet ping failure explanation
- Two different networks.

