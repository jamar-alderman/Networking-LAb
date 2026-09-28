# Floor 2 core-uplink ARP drop

## Symptom

Both Floor 2 core links showed `up/up` and connected /30 routes, but ping to the directly connected peers .9 and .13 failed 0/5. No peer ARP entry appeared on Floor 2. CORE-2 could ARP for Floor 1 .6 but could not ARP for Floor 2 .14.

## Investigation

Running configs showed routed Gigabit interfaces and `ip routing`. The /30 masks and interface IP assignments matched the intended map, but the actual physical cables did not connect the documented port pairs. In Packet Tracer Simulation mode, an ARP request from Floor 2 source **10.255.0.14** for **10.255.0.13** was shown arriving at a device displayed as `CORE-FLOOR 1` on **Gi0/2**. Its PDU explanation stated that the sender IP address was in a different network than the receiving port and that the ARP frame was dropped. It also explicitly said DAI validation was bypassed. VLAN 1 membership of the core's unused Fa ports did not cause this routed-port ARP failure.

That simulation event showed a port/subnet mismatch: an ARP sender from one /30 reached a receiving port in another /30. The intended diagram and running configurations were correct; the cable endpoints were not aligned with them during the failure. An earlier CDP snapshot appeared to show the expected peer, so the final physical map should still be documented with post-fix neighbor output.

## Resolution status

The builder identified the root cause as physical cables connected to ports different from those in the documented core-to-distribution map. They moved the cables to match the map without changing the IP assignments and report that direct pings then worked. This is a user-reported resolution; post-fix CDP and passing ping transcripts have not yet been added. Do not infer DHCP, inter-floor routing, or tested failover from the direct-link repair.
