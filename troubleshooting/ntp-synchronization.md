# NTP synchronization delay

## Problem

The switch initially reported unsynchronized NTP status.

## Investigation / evidence

Server0 at `192.168.10.5` had NTP enabled, and the switch used `ntp server 192.168.10.5`.

## Resolution

Time elapsed before status was checked again; no additional configuration change is evidenced.

## Verification / current state

The later status reported a synchronized clock, stratum 2, reference `192.168.10.5`, and a recent update. `show clock` updated to Aug 2, 2026. See [NTP verification](../verification/ntp-verification.md).

**TODO:** Add the complete before/after status and clock captures.
