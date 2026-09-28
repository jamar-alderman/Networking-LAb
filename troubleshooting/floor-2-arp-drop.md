# Floor 2 core-uplink ARP drop

## Symptom

Both Floor 2 core links showed `up/up` and connected /30 routes, but ping to the directly connected peers .9 and .13 failed 0/5. No peer ARP entry appeared on Floor 2. CORE-2 could ARP for Floor 1 .6 but could not ARP for Floor 2 .14.

## Investigation

Running configs showed routed Gigabit interfaces and `ip routing`. The /30 masks and address pairs were mathematically valid, but the distribution port-to-IP assignments did not match the actual physical core connections. In Packet Tracer Simulation mode, an ARP request from Floor 2 source **10.255.0.14** for **10.255.0.13** was shown arriving at a device displayed as `CORE-FLOOR 1` on **Gi0/2**. Its PDU explanation stated that the sender IP address was in a different network than the receiving port and that the ARP frame was dropped. It also explicitly said DAI validation was bypassed. VLAN 1 membership of the core's unused Fa ports did not cause this routed-port ARP failure.

That simulation event showed a port/subnet mismatch: an ARP sender from one /30 reached a receiving port in another /30. The initial diagram and running configurations did not capture the effective physical-to-IP mapping. An earlier CDP snapshot appeared to show the expected peer, so the exact final interface map should be verified from post-fix output.

## Resolution status

The builder identified the root cause as the distribution uplink IP addresses mapped backwards relative to the physical core connections, corrected those distribution interface IP assignments, and reports that the direct pings then worked. This is a user-reported resolution; the final `show ip interface brief` / CDP map and passing ping transcript have not yet been added. Do not infer DHCP, inter-floor routing, or tested failover from the direct-link repair.
