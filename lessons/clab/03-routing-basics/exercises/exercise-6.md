Interface Status output disabled link:
```
docker exec -it clab-routing-basics-srl1 sr_cli -c "show interface brief | grep -v enable"
+---------------------+---------------------+---------------------+---------------------+---------------------+---------------------+
|        Port         |     Admin State     |     Oper State      |        Speed        |        Type         |     Description     |
+=====================+=====================+=====================+=====================+=====================+=====================+
| ethernet-1/3        | disable             | down                | 25G                 |                     |                     |
```

Explanation of why a route's existence does not guarantee path availability:
After disabling ethernet-1/3 on srl1, host1 can no longer reach host3. ethernet-1/3 is the interface on srl1 connected toward srl3 over the 10.1.3.0/24 network.

The route to 10.1.5.0/24 may still exist in the routing table because it is a configured static route. However, the next-hop for that route is reached through ethernet-1/3. Since ethernet-1/3 is admin-disabled, srl1 cannot forward packets out that interface toward srl3.

This shows that route existence does not guarantee path availability. A route can be present in the routing table, but forwarding can still fail if the outgoing interface or next-hop is unreachable.
