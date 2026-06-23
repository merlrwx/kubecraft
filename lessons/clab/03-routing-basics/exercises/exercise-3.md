The route missing from srl2 is the static route to 10.1.5.0/24.

host2 -> host3 fails because host2 sends traffic to its default gateway srl2, but srl2 no longer has a route to 10.1.5.0/24, so it cannot forward the packet toward srl1/srl3.

host3 -> host2 also fails because ping requires a return packet. The echo request from host3 may reach host2 through srl3 -> srl1 -> srl2, but host2's echo reply must go back through srl2. Since srl2 is missing the route to 10.1.5.0/24, the reply cannot return to host3.

host1 -> host3 still works because that traffic does not use srl2. It goes from host1 to srl1, then from srl1 to srl3, and srl3 is directly connected to 10.1.5.0/24.
