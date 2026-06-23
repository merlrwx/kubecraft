Black hole explanation:

host1 sends traffic for 10.1.5.2 to srl1. srl1 has a static route for 10.1.5.0/24, so the route appears valid in the routing table. However, the static route points to next-hop 10.1.3.99 instead of the real srl3 address 10.1.3.2.

srl1 tries to resolve 10.1.3.99 using ARP on the 10.1.3.0/24 link. The ARP table shows 10.1.3.99 with MAC address 00:00:00:00:00:00 and expiry “now”, meaning ARP resolution failed. Since srl1 cannot map the next-hop IP to a MAC address, it cannot send the frame to the next router. The packet is dropped/black-holed at srl1.

ARP Output:
```
docker exec -it clab-routing-basics-srl1 sr_cli -c "show arpnd arp-entries"
+-------------+-------------+----------------+-------------+-------------------------+------------------------------------------------+
|  Interface  | Subinterfac |    Neighbor    |   Origin    |   Link layer address    |                     Expiry                     |
|             |      e      |                |             |                         |                                                |
+=============+=============+================+=============+=========================+================================================+
| ethernet-   |           0 |       10.1.1.2 |     dynamic | AA:C1:AB:99:EF:07       | 3 hours from now                               |
| 1/1         |             |                |             |                         |                                                |
| ethernet-   |           0 |       10.1.2.2 |     dynamic | 1A:50:04:FF:00:01       | an hour from now                               |
| 1/2         |             |                |             |                         |                                                |
| mgmt0       |           0 |    172.20.20.1 |     dynamic | E6:49:2E:EE:98:52       | an hour from now                               |
+-------------+-------------+----------------+-------------+-------------------------+------------------------------------------------+
```
The route to 10.1.5.0/24 still exists on srl1, so at first glance the routing table looks okay.

However, the static route depends on a next-hop group, and that next-hop has been changed to 10.1.3.99.

10.1.3.99 is in the 10.1.3.0/24 link, so srl1 tries to ARP for it out ethernet-1/3. But no device actually owns 10.1.3.99, so ARP cannot resolve a real MAC address.

In the ARP table, the entry for 10.1.3.99 shows 00:00:00:00:00:00 and expiry “now”, which indicates failed/unresolved ARP.

Because srl1 cannot resolve the next-hop to a MAC address, it cannot actually forward the packet. The route exists, but traffic is effectively black-holed at srl1.



Key Lesson:
A route can exist in the routing table, but forwarding still fails if the next-hop cannot be resolved at Layer 2.

