1. Check the routing table:
`docker exec clab-ip-fundamentals-host1 ip route show`

2. Notice: only the 10.1.1.0/24 route exists (directly connected). No default route.

3. Explain: Why does 10.1.1.1 work but 10.1.2.1 doesn't?

4. Fix by restoring the default route:
`docker exec clab-ip-fundamentals-host1 ip route add default via 10.1.1.1 dev eth1`

5. Verify: ping 10.1.2.1 now works (srl1 has that subnet directly connected).

A host can directly reach devices on its local subnet.
Without a gateway, host1 does not know where to send traffic for remote subnets.

A local subnet is the network your device is directly connected to.

A remote subnet is any network your device is not directly connected to.

Local subnet = reachable directly
Remote subnet = needs a gateway/router
