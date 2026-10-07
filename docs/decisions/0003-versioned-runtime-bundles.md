# ADR 0003: Versioned runtime bundles

**State:** Accepted  
**Date:** 2026-10-07

## Context

Wine, DXMT, DLL integration, prefix state, environment variables, Steam/CS2
versions, macOS, and Apple Silicon behavior interact. Independently updating
one component can break a working setup.

## Decision

Treat the compatible Wine build, DXMT build, integration mode, prefix schema,
launch environment, checksums, constraints, and known issues as one immutable
runtime definition.

Channels (`stable`, `candidate`, `experimental`) point to tested runtime IDs.
CSilicon never silently replaces a working runtime merely because an upstream
version is newer.

## Consequences

- Manifests, artifact verification, atomic activation, and rollback are core.
- Disk usage is higher because old working runtimes are retained temporarily.
- Promotion needs evidence from a declared support matrix.
- Emergency revocation needs signed catalog metadata and clear user messaging.
