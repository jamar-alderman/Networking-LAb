# DHCP snooping experiment

## Symptom

PCs and phones received DHCP addresses before snooping was enabled. Enabling global DHCP snooping on the test access switch caused lease renewal to fail; disabling it restored DHCP.

## Investigation

1. Enabled snooping for VLANs 10 and 20.
2. Attempted trust on Port-channel1 and later Port-channel2. Packet Tracer rejected `ip dhcp snooping trust` on the logical interface.
3. Applied trust to Fa0/19–21. Show output confirmed those ports trusted, but the tested switch's uplink was actually Po2.
4. Corrected trust to the actual Po2 members, Fa0/22–24.
5. A successful renewal initially appeared to resolve the issue, but global snooping was still disabled during that renewal.
6. Re-enabled snooping globally; DHCP failed again despite the corrected physical-port trust.
7. Disabled snooping to restore working DHCP and deferred DAI.

## Outcome and lesson

DHCP snooping is not part of the working configuration. The exact cause of the remaining failure was not proven; it should not be attributed conclusively to EtherChannel or a simulator defect. The observed status showed Option 82 insertion enabled, but its role in the failure was not isolated.

Trust must follow the actual server-facing ingress path, and a passing DHCP test only verifies snooping when snooping is enabled. Checking global feature state prevented a false success claim.
