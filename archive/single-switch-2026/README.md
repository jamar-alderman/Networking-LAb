# Enterprise Campus Network Lab

A Cisco Packet Tracer lab emulating a small campus or branch network. I configured a 3560-type multilayer switch to separate endpoint functions into VLANs, route between their subnets, relay DHCP to one server, and support voice, wireless, management, and access security. This repository records the configuration facts, observed switch output, troubleshooting, and gaps in the available evidence.

> **Environment:** Simulation in Cisco Packet Tracer. This is not a production deployment.

## Topology and architecture

**TODO:** Add an overall Packet Tracer topology screenshot showing the switch, Server0, IP phones and PCs, access points, and wireless client. See [topology notes](topology/README.md). The screenshot has not been supplied yet.

Server0 (`192.168.10.5`) is directly connected to switch `Gi0/1` in VLAN 25. The switch provides the known SVI gateways below. Remote VLANs can forward DHCP requests to Server0 through `ip helper-address`; phone and PC connections on `Fa0/6`–`Fa0/8` use separate voice and data VLANs. AccessPoint-PT devices and a wireless laptop/client are present in the topology; their exact interface, SSID, addressing, and client test results are pending evidence. There is no gateway of last resort in this contained lab.

| VLAN | Observed name / purpose | Subnet | SVI / gateway |
| --- | --- | --- | --- |
| 25 | ENDusrs / end users | 192.168.10.0/24 | 192.168.10.1 |
| 30 | VOICE | 192.168.30.0/24 | 192.168.30.1 |
| 35 | MNGMNT | Not established | Not established |
| 45 | MNGMNTUSRS | 192.168.9.0/24 | 192.168.9.1 |
| 101 | ACL | 192.168.20.0/24 | 192.168.20.1 |
| 200 | OTHERS | 192.168.99.0/24 | 192.168.99.1 |

The VLAN ID does not necessarily match the subnet's third octet. VLAN 35's name is known, but its subnet and gateway have not been established.

## Implemented features and evidence

### Layer 3 switching

The multilayer switch provides SVI gateways and inter-VLAN routing. The observed routing table included connected routes for `192.168.9.0/24` on Vlan45, `192.168.10.0/24` on Vlan25, `192.168.20.0/24` on Vlan101, `192.168.30.0/24` on Vlan30, and `192.168.99.0/24` on Vlan200. The relevant SVIs eventually showed `up/up`. These observations show switch routing state; per-host reachability tests have not been supplied. [Routing evidence](verification/routing-verification.md) · [VLAN/SVI evidence](verification/vlan-and-svi-verification.md)

**TODO:** Add the VLAN/SVI screenshot and unabridged `show vlan brief`, `show ip interface brief`, and `show ip route` output.

### Centralized DHCP and relay

Server0 at `192.168.10.5` provides DHCP on the VLAN 25 network. Remote SVIs include relay configuration; for example:

```ios
interface Vlan30
 ip address 192.168.30.1 255.255.255.0
 ip helper-address 192.168.10.5
```

This SVI is the voice gateway and forwards DHCP requests to Server0. Vlan45 also has a helper to the same server. The voice scope uses `192.168.30.0/24`, gateway `192.168.30.1`, DNS `8.8.8.8`, and a starting address observed/configured around `192.168.30.6`; the exact starting address needs a Server0 screenshot. PCs behind phones receive VLAN 25 addresses; phones are intended for VLAN 30. [Relay configuration](configs/dhcp-relay.txt) · [Troubleshooting notes](troubleshooting/dhcp-relay.md)

**TODO:** Add the DHCP relay/routing screenshot, Server0 scope details, and client lease evidence. The supplied summary does not establish exact client leases or a complete DHCP transaction test.

### Voice and data access

`Fa0/6`, `Fa0/7`, and `Fa0/8` use data VLAN 25 and voice VLAN 30 for a phone with a downstream PC. The representative `Fa0/7` configuration is in [voice/access configuration](configs/voice-and-access-ports.txt). MAC-table entries were observed in VLAN 25 and VLAN 30 on `Fa0/7` and `Fa0/8`; Vlan30 changed from `up/down` to `up/up` after phone/link/power troubleshooting. These observations support VLAN learning and SVI state, but do not by themselves prove a phone acquired a particular IP address. [Voice verification](verification/voice-vlan-verification.md)

**TODO:** Add a voice/access screenshot and client-side addressing or call evidence if available.

### Port security

`Fa0/7` uses sticky MAC learning, a maximum of three secure MAC addresses, and `restrict` violation mode. The limit was **initially two**; phone+PC MAC learning generated violations, so it was increased to three. The later `Fa0/7` output showed `Secure-up`, two secure/sticky MACs, and a historical violation count of six. Protect, Restrict, and Shutdown behavior was tested in broader lab work, but detailed output for each mode is still needed. [Configuration](configs/port-security.txt) · [Observed status](verification/port-security-verification.md) · [Troubleshooting](troubleshooting/port-security-violations.md)

### DHCP snooping

DHCP snooping was enabled and configured for VLANs 25, 30, and 45. `Gi0/1`, connected to Server0, was marked trusted; client-facing FastEthernet ports were untrusted. **The observed `show ip dhcp snooping` output reported operational VLANs as `none`** despite showing the configured VLANs. This repository therefore records the configuration and observed trust state, without claiming operational enforcement. [Configuration](configs/dhcp-snooping.txt) · [Verification and limitation](verification/dhcp-snooping-verification.md)

**TODO:** Add the full DHCP snooping output and a screenshot with the configured and operational VLAN fields visible.

### NTP, SSH, ACLs, and wireless

Server0 provides NTP. The switch uses `ntp server 192.168.10.5`; after an initial unsynchronized state it reported `Clock is synchronized, stratum 2, reference is 192.168.10.5`. [NTP evidence](verification/ntp-verification.md)

SSH remote management was configured, but its exact commands and a login verification are not yet supplied. `Fa0/1` was observed with inbound `ip access-group 10 in`; the ACL entries and traffic tests are not supplied. Wireless access points and a wireless client are in the topology, with exact settings pending. [SSH and ACL notes](configs/ssh-and-acl-notes.txt)

**TODO:** Add NTP status/clock screenshot, sanitized SSH configuration and login result, ACL definition and test output, and wireless configuration/connectivity evidence.

## Verification approach

Configuration snippets record settings; switch `show` output records reported state. Available observations are summarized under [verification](verification/README.md). The next evidence pass should capture the complete sanitized `show running-config`, `show vlan brief`, `show ip interface brief`, `show ip route`, `show mac address-table`, `show port-security`, both `Fa0/7` and `Fa0/8` port-security details, `show ip dhcp snooping`, `show ntp status`, and `show clock`.

## Troubleshooting highlights

| Issue | Evidence and action | Later observed state |
| --- | --- | --- |
| Phone+PC MAC learning exceeded limit of two | Restrict-mode violations; maximum changed to three | `Fa0/7` Secure-up, two sticky/secure MACs, six historical violations |
| Voice SVI was `up/down` | Phone power and link investigated; `%ILPOWER-5-IEEE_DISCONNECT` appeared during power changes | Green links; Vlan30 `up/up`; connected voice route present |
| NTP initially unsynchronized | Waited and checked status again | Synchronized at stratum 2 to `192.168.10.5` |
| DHCP snooping operational state unclear | Compared configured VLANs, trust state, and operational VLAN field | Configured 25/30/45; operational `none` in observed output |

See the [troubleshooting notes](troubleshooting/README.md) for supported details. Address/subnet overlap was encountered during broader work; exact values and resolution steps await evidence.

## Known limits and lessons

- This is a Packet Tracer simulation. Device behavior and command support may differ from physical equipment. In this workflow, `show mac address-table vlan 30` was not accepted, so the full MAC table was inspected.
- DHCP snooping configuration and port trust were observed; operational VLANs were reported as `none`. Enforcement is unverified.
- SVI and routing-table state do not establish every end-to-end client test. Exact phone lease, wireless connection, SSH login, and ACL results need evidence.
- Voice SVI state depended on an active voice-side link in this lab. A historical port-security violation count persisted after the later Secure-up state. NTP required time and a second status check before synchronization appeared.
- `Fa0/2` was observed with `switchport voice vlan 35`, likely an accidental voice assignment given VLAN 35's MNGMNT name. Its correction is recommended only if no phone is intended there; a completed correction has not been evidenced.

## Repository navigation

| Path | Contents |
| --- | --- |
| [topology/](topology/README.md) | Device relationships and screenshot TODO |
| [configs/](configs/README.md) | Supplied IOS snippets and configuration gaps |
| [verification/](verification/README.md) | Observed output summaries and requested full captures |
| [troubleshooting/](troubleshooting/README.md) | Problem, investigation, and current-state narratives |
| [screenshots/](screenshots/README.md) | Screenshot checklist and captions |
