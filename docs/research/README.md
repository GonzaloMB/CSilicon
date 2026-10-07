# Research plan

**State:** Proposed  
**Owner:** Project maintainers  
**Active:** Yes

## Questions this phase must answer

1. Can a supported Apple Silicon Mac reproducibly execute the required
   x86_64 Windows, Direct3D 11, Steam, and CS2 path?
2. Which component boundaries and versions produce a known-good baseline?
3. Which parts may CSilicon download, build, modify, and redistribute?
4. Which signals can be collected without touching the game process?
5. Can VAC-secure matchmaking operate normally with untouched game files, and
   what safety limits must CSilicon enforce?
6. What minimum host support matrix is honest and testable?

## Workstreams

| ID | Workstream | Output |
|---|---|---|
| R1 | Execution route | evidence-based macOS/VM/Asahi route decision |
| R2 | Wine and DXMT | compatible component matrix and smoke tests |
| R3 | Steam and CS2 | offline launch, update, input, audio, and rendering report |
| R4 | VAC and online safety | explicit supported/unsupported policy |
| R5 | Diagnostics | observable signals and redaction inventory |
| R6 | Supply chain and licensing | source, license, checksum, and distribution policy |
| R7 | Performance | repeatable benchmark method and noise controls |
| R8 | Distribution | signing, notarization, update, and rollback requirements |

## Method

For every result, record:

- date, host model, macOS build, and architecture;
- exact artifact versions and SHA-256 digests;
- runtime manifest and relevant environment variables;
- numbered reproduction steps;
- expected and observed result;
- logs and run ID;
- evidence grade and remaining uncertainty.

Do not convert a community workaround into a default configuration until it is
reproduced. Do not use personal Steam identifiers, credentials, or account
tokens in committed evidence.

## Exit criteria

Phase 1 completes only when:

- at least one full offline/insecure launch path is reproduced twice from a
  clean CSilicon-owned prefix;
- a failed runtime activation is rolled back without harming the working one;
- component licenses and permitted distribution mode are documented;
- diagnostic capture and redaction are demonstrated on real logs;
- VAC-secure matchmaking is tested without modifying protected files, or is
  explicitly classified as unsupported with the product impact documented;
- open blockers have owners and do not invalidate Milestone 0 (`doctor`).
- results are expressed as a support matrix, not assumptions derived from one
  developer machine.
