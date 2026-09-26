# DHCP relay design and investigation

## Problem / design need

Remote VLANs require DHCP service from Server0 on VLAN 25 rather than a DHCP server in each VLAN.

## Investigation / evidence

Vlan30 and Vlan45 configuration includes `ip helper-address 192.168.10.5`. Server0's voice scope is summarized in [configuration](../configs/dhcp-relay.txt). Addressing/subnet overlap was encountered during broader lab work, but exact conflicting values and diagnostic steps are not supplied.

## Resolution / current state

The supplied configuration points both remote SVIs to the centralized server. PCs behind phones receive VLAN 25 addresses and phones are intended for VLAN 30, according to the supplied lab summary. Exact leases and a complete DHCP relay transaction trace remain unverified here.

**TODO:** Add Server0 scope, SVI output, client lease captures, and precise troubleshooting steps if available.
