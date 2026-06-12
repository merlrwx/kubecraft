`show interface brief`:
ethernet-1/1        | disable | down   | 25G 

To fix:
```
enter candidate
set / interface ethernet-1/1 admin-state enable
commit now
```

Result:
❯ docker exec clab-ip-fundamentals-host1 ping -c 3 10.1.1.1
# FAILS -- no response
PING 10.1.1.1 (10.1.1.1): 56 data bytes
64 bytes from 10.1.1.1: seq=0 ttl=64 time=4.278 ms
64 bytes from 10.1.1.1: seq=1 ttl=64 time=1.268 ms
64 bytes from 10.1.1.1: seq=2 ttl=64 time=2.254 ms

--- 10.1.1.1 ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 1.268/2.600/4.278 ms
