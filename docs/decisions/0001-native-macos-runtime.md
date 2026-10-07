# ADR 0001: Native macOS runtime

**State:** Accepted  
**Date:** 2026-10-07

## Context

Wine, DXMT, Metal, CPU translation, process management, and real GPU access are
the compatibility path itself. Adding a Linux VM/container boundary makes host
graphics and process behavior less direct and introduces another environment
to diagnose.

## Decision

Steam, CS2, Wine, DXMT, CPU translation, and local inference execute directly
on macOS. Docker is not a CSilicon runtime dependency.

Docker may later be used for unrelated CI services or test doubles only when a
specific need exists.

## Consequences

- Host detection and macOS-specific adapters are first-class.
- Tests must include real Apple Silicon hardware.
- Packaging, signing, and notarization become project concerns.
- Linux-container reproducibility cannot substitute for runtime validation.
