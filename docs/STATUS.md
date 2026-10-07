# Project status

**Updated:** 2026-10-07  
**Status:** Researching  
**Active phase:** Phase 1 — technical feasibility  
**Implementation status:** Not started

## Established so far

- The product objective includes normal CS2 online play and matchmaking, not
  merely reaching the menu or running offline.
- “Online” means Valve matchmaking/Premier. FACEIT is not feasible because its
  required anti-cheat is officially available only for Windows 10/11 and
  requires Windows security features unavailable through Wine.
- CSilicon is macOS-native; Docker is not part of the runtime path.
- The target is Apple Silicon, with Counter-Strike 2 left untouched.
- The core is planned in Rust and begins as a CLI.
- Wine, DXMT, prefix settings, and launch configuration form one immutable,
  versioned runtime definition.
- Diagnostics, privacy, reversibility, and supply-chain verification are
  product requirements rather than later enhancements.
- AI is optional and cannot precede a stable non-AI workflow.
- Linux in a macOS VM is not a viable graphics path with Apple's documented
  Virtio GPU 2D support.
- Bare-metal Asahi Linux has a device-dependent support matrix and would
  require leaving macOS, so it cannot be the general CSilicon runtime.

## Not established yet

- A known-good Wine/DXMT/Steam/CS2 combination.
- The exact macOS and chip support matrix.
- Whether secure online matchmaking works safely and reliably.
- Runtime redistribution and licensing terms.
- Performance, input latency, audio, controller, and crash behavior.
- The exact persistence schema and whether SQLite is needed in early releases.

## Current objective

Produce a reproducible feasibility report from controlled experiments. The
first implementation milestone is authorized only after the Phase 1 gate in
[the roadmap](roadmap/phases.md) is satisfied.

The CrossOver 26.3 reference artifact has been acquired from the official
CodeWeavers distribution, checksum-verified, code-signature-verified, and
accepted by Gatekeeper. An initial setup attempt was canceled before Steam
authentication or any CS2 download, and the local reference environment was
removed. No runtime feasibility result can be inferred from that attempt.

## Next actions

1. Repeat the time-limited CrossOver reference experiment on a dedicated test
   host, without packaging proprietary components into CSilicon.
2. Create a dedicated CS2 reference bottle for that experiment.
3. Record whether Steam, CS2, audio, input, rendering, and clean shutdown work.
4. Validate game-file integrity before any online experiment.
5. Evaluate VAC-secure matchmaking separately, with explicit user consent and
   no injection, patching, hooking, or debugger attachment.
6. Compare the working reference with candidate redistributable Wine/DXMT
   runtimes from trusted upstreams.
7. Repeat validated experiments across the declared Apple Silicon support
   matrix before making compatibility claims.
