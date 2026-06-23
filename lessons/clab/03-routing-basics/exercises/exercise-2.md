Written hop-by-hop trace for host2 -> host3 AND the return path

host2 -> host3

host2 sends traffic for 10.1.5.2 to its default gateway, srl2.

srl2 looks up 10.1.5.0/24 and finds a static route via the 10.1.2.0/24 link toward srl1.

srl1 looks up 10.1.5.0/24 and finds a static route via the 10.1.3.0/24 link toward srl3.

srl3 has 10.1.5.0/24 as a local/directly connected route, so it forwards the packet directly to host3.



host3 -> host2

host3 sends traffic for 10.1.4.2 to its default gateway, srl3.

srl3 looks up 10.1.4.0/24 and finds a static route via the 10.1.3.0/24 link toward srl1.

srl1 looks up 10.1.4.0/24 and finds a static route via the 10.1.2.0/24 link toward srl2.

srl2 has 10.1.4.0/24 as a local/directly connected route, so it forwards the packet directly to host2.

