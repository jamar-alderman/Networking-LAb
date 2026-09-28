# Floor 2 core-uplink ARP drop

## Symptom

Both Floor 2 core links showed `up/up` and connected /30 routes, but ping to the directly connected peers .9 and .13 failed 0/5. No peer ARP entry appeared on Floor 2. CORE-2 could ARP for Floor 1 .6 but could not ARP for Floor 2 .14.

## Investigation

Running configs showed routed Gigabit interfaces, `ip routing`, and correct addresses and masks on CORE-2 and DISTRIBUTION-FLOOR-2. In Packet Tracer Simulation mode, an ARP request from Floor 2 source **10.255.0.14** for **10.255.0.13** was shown arriving at a device displayed as `CORE-FLOOR 1` on **Gi0/2**. Its PDU explanation stated that the sender IP address was in a different network than the receiving port and that the ARP frame was dropped. It also explicitly said DAI validation was bypassed. VLAN 1 membership of the core's unused Fa ports did not cause this routed-port ARP failure.

That simulation event indicates the packet reached a receiving port inconsistent with the intended `10.255.0.13` port (CORE-2 Gi0/1). Canvas labels may differ from CLI hostnames, and an earlier CDP snapshot appeared to show the expected peer. This is evidence of a port/IP mismatch **for the captured event**, not proof of exactly when or how a cable was changed.

## Resolution status

The user later reported that core links speak to the distributions. A post-change PDU trace, final CDP map, and passing bidirectional ping output are still needed to document the exact correction. Do not claim DHCP, inter-floor routing, or tested failover from this event.
