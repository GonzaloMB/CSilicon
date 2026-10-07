# Target machine

**Captured:** 2026-10-07  
**Evidence:** Reproduced, read-only host inventory

Only the minimum non-sensitive facts needed for compatibility research are
recorded here. Serial number, hardware UUID, provisioning ID, username, and
other direct identifiers are intentionally excluded.

| Property | Value |
|---|---|
| Product | MacBook Pro |
| Model identifier | `Mac16,8` |
| Chip | Apple M4 Pro |
| CPU cores | 12 (8 performance, 4 efficiency) |
| Unified memory | 24 GB |
| Architecture | `arm64` |
| macOS | 26.6.2 |
| macOS build | 25G83 |
| System Integrity Protection | Enabled |

## Route implications

- The hardware is comfortably above the memory levels in CodeWeavers' older
  successful M3 Pro/18 GB CS2 test, but that does not predict current frame
  rate or compatibility.
- Current Asahi documentation identifies `Mac16,8` as an M4 Pro device, with no
  installer and no GPU support. Bare-metal Linux is not a usable test route.
- macOS/Wine remains the only local, accelerated candidate for this target.

## Privacy note

Future `doctor` implementation must query only required fields or redact the
raw output before it is logged. Broad `system_profiler` output includes direct
device and user identifiers and must never be stored in a run record or
diagnostic bundle.
