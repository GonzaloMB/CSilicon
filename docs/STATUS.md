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
- Bare-metal Asahi Linux is not currently installable or GPU-capable on the
  target M4 Pro MacBook Pro (`Mac16,8`).

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

## Next actions

1. Establish CrossOver 26.3 as a reference baseline on the target Mac without
   changing or packaging its proprietary components.
2. Record whether Steam, CS2, audio, input, rendering, and clean shutdown work.
3. Validate game-file integrity before any online experiment.
4. Evaluate VAC-secure matchmaking separately, with explicit user consent and
   no injection, patching, hooking, or debugger attachment.
5. Compare the working reference with candidate redistributable Wine/DXMT
   runtimes from trusted upstreams.
