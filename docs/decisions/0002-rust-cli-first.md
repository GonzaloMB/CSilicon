# ADR 0002: Rust core and CLI-first delivery

**State:** Accepted  
**Date:** 2026-10-07

## Context

The critical path needs predictable process supervision, typed state
transitions, low runtime dependency, and native macOS distribution. A UI would
hide unresolved runtime behavior rather than reduce the initial risk.

## Decision

Build the core in Rust. Deliver a small CLI before any GUI. Begin with one Rust
package and internal modules; split crates only for demonstrated boundaries.

Python is not required to launch or diagnose CS2. A future Tauri/React UI may
reuse an extracted Rust core after the CLI behavior is stable.

## Consequences

- Milestone 0 is `cargo build` plus read-only `csilicon doctor`.
- UI work does not block compatibility research.
- Dependency additions require a concrete operational benefit.
- macOS APIs may require narrow, reviewed FFI or maintained Rust bindings.
