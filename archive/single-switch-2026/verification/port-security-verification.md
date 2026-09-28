# Port-security verification

The later `Fa0/7` output was summarized as:

| Field | Observed value |
| --- | --- |
| Port security | Enabled |
| Port status | Secure-up |
| Violation mode | Restrict |
| Maximum MAC addresses | 3 |
| Total secure MAC addresses | 2 |
| Sticky MAC addresses | 2 |
| Violation count | 6, historical |

The count reflects earlier violations when the limit was two; it does not establish six current failures in the later Secure-up state. Protect, Restrict, and Shutdown behavior was tested/observed during broader work, but the exact per-mode output has not been supplied.

**TODO:** Add full `show port-security`, `show port-security interface fa0/7`, and `show port-security interface fa0/8` captures, plus a voice/port-security screenshot.
