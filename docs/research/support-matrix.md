# Apple Silicon support matrix

**State:** Draft

CSilicon compatibility claims are made for classes of Macs, not for one
developer machine. No serial numbers, hardware UUIDs, local usernames, device
management state, or other machine-specific identifiers belong in this file.

## Dimensions

Each validated configuration records only the compatibility dimensions needed
to reproduce behavior:

- Apple chip family and tier;
- macOS major/minor version and supported range;
- total memory tier;
- Metal feature family relevant to the selected backend;
- Wine and DXMT runtime ID;
- Steam client channel/build;
- CS2 build ID;
- display resolution class and refresh-rate class;
- cold/warm shader-cache state;
- outcome for setup, launch, input, audio, shutdown, and matchmaking.

## Planned coverage classes

| Class | Purpose | Status |
|---|---|---|
| Base Apple Silicon | establish minimum supported memory/GPU floor | research needed |
| Pro-tier Apple Silicon | primary performance and stability profile | research needed |
| Max/Ultra-tier Apple Silicon | high-end scaling and multi-display behavior | research needed |
| Current macOS release | primary supported OS | research needed |
| Previous macOS release | compatibility and upgrade safety | research needed |
| Next macOS preview | early warning only; never stable by default | deferred |

Exact chip generations and OS versions are added only after reproduced tests.
An untested family reports `unknown`, never “supported by similarity.”

## Result states

- `supported`: all applicable release gates pass on the declared class.
- `candidate`: repeated success, but coverage or long-run evidence is incomplete.
- `degraded`: launches with documented missing functionality or performance.
- `unsupported`: a known blocker prevents the product goal.
- `unknown`: no adequate reproduced evidence.

## Privacy and publication

Published reports contain normalized classes and runtime/build identifiers.
Raw host-tool output is not committed. Local evidence must be sanitized before
publication, and exact device identifiers are discarded rather than merely
redacted at export time.
