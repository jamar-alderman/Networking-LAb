# NTP verification

Server0 at `192.168.10.5` had NTP enabled, and the switch was configured with `ntp server 192.168.10.5`. It initially reported unsynchronized state. After waiting, the supplied status excerpt reported:

```text
Clock is synchronized, stratum 2, reference is 192.168.10.5
...
last update was a few seconds ago
```

`show clock` then updated to Aug 2, 2026. The omitted middle lines above are explicitly elided, not reconstructed output.

**TODO:** Add complete `show ntp status` and `show clock` output and the NTP screenshot.
