# Provisional system design

**State:** Draft  
**Depends on:** Phase 1 feasibility evidence

## Context

```text
User
  |
  v
CSilicon CLI
  |
  +-- host inspection / doctor
  +-- runtime acquisition and activation
  +-- prefix lifecycle
  +-- launch and process supervision
  +-- structured diagnostics and export
  |
  v
Immutable runtime bundle
  +-- compatible Wine build
  +-- compatible DXMT build
  +-- validated launch environment
  +-- prefix schema/template
  +-- signed/checksummed manifest
  |
  v
Steam -> untouched CS2 binaries
  |
  +-- CPU path: Wine + Apple translation capability
  +-- graphics path: D3D11 -> DXMT -> Metal
  v
macOS / Apple Silicon
```

The diagram is conceptual. Phase 1 must verify the precise CPU and process
boundaries rather than encoding an assumed Rosetta topology. The Linux build
was evaluated separately and rejected as the primary product route because a
Linux VM lacks the documented accelerated graphics path and bare-metal Linux
cannot provide a consistent experience from macOS across Mac generations.

## Architectural style

Start with one Rust package containing a library and a thin binary. Use clear
modules and dependency boundaries; do not begin with multiple crates merely to
look modular.

```text
CLI -> application use cases -> domain types and ports
                               ^
                               |
                 adapters: macOS, filesystem, process, network
```

The domain describes desired behavior without shelling out. Platform adapters
perform macOS and process operations. This keeps detection logic testable and
makes every modifying operation visible at the application boundary.

## State locations

The exact layout remains a Phase 2 decision. The default proposal is:

```text
~/Library/Application Support/CSilicon/
├── config/config.toml
├── manifests/
├── runtimes/<runtime-id>/
├── prefixes/cs2/
├── runs/<run-id>/events.jsonl
├── diagnostics/
└── state/                 # SQLite only if justified
```

Large disposable caches may move to `~/Library/Caches/CSilicon/` after testing
cleanup and backup expectations. Secrets are never stored in either location.

## Invariants

- Runtime directories are immutable after verification.
- Activation changes a small pointer/reference, not runtime contents.
- Downloads land in staging and cannot execute before verification.
- Prefix migrations are versioned and recoverable.
- Every launch has a unique run ID before child processes start.
- Structured events are the canonical log; console text is a rendered view.
- Export always passes through redaction and shows the user what will leave.
- Unknown manifest fields and incompatible constraints fail closed.
- The runtime never depends on Docker or a cloud service.

## Runtime activation state machine

```text
declared -> downloaded -> checksum_verified -> unpacked -> validated
                                                        |
                                                        v
working <---------------- rollback <--- activating -> active
```

A crash at any point must leave either the old active runtime or a clearly
recoverable staged runtime. It must never produce a half-mutated active bundle.

## Persistence strategy

Begin with atomic manifest/config files and append-only JSON Lines run events.
Introduce SQLite when queries across runs, benchmarks, or experiments justify
it. This avoids an unnecessary schema and migration burden in Milestone 0 while
preserving a path to indexed local history.

## Future AI boundary

An optional advisor may call typed capabilities only after Milestones 0–4. It
may propose a reversible experiment, but modifying actions require explicit
confirmation. It cannot invent artifact sources or execute arbitrary shell.
