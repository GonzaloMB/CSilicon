# CSilicon documentation

This directory is the source of truth while CSilicon is being researched and
designed. Implementation must follow accepted decisions here; assumptions must
not silently become product behavior.

## Current phase

We are in **Phase 1 — technical feasibility research**. No production runtime,
installer, launcher, or AI layer should be implemented until the phase exit
criteria are met.

- [Project status](STATUS.md)
- [Vision and scope](product/vision-and-scope.md)
- [Research plan](research/README.md)
- [Initial findings](research/initial-findings.md)
- [Execution route comparison](research/execution-routes.md)
- [Sanitized target machine](research/target-machine.md)
- [Research backlog](research/backlog.md)
- [Experiment protocol](research/experiment-protocol.md)
- [Provisional system design](architecture/system-design.md)
- [Provisional module map](architecture/modules.md)
- [Runtime manifest proposal](architecture/runtime-manifest.md)
- [Delivery phases](roadmap/phases.md)
- [Release gates](roadmap/release-gates.md)
- [Architecture decisions](decisions/README.md)

## Document states

Every architectural document uses one of these states:

- **Draft**: useful working hypothesis; may change without migration work.
- **Proposed**: ready for review and validation.
- **Accepted**: binding until superseded by another recorded decision.
- **Superseded**: retained for history but no longer active.

Research evidence is classified as:

1. **Primary** — vendor or upstream documentation/source.
2. **Reproduced** — observed in a repeatable CSilicon experiment.
3. **Community** — useful signal that still requires reproduction.
4. **Assumption** — unverified and never sufficient for a release decision.

## Working rule

Research produces evidence. Evidence informs decisions. Accepted decisions
constrain implementation. If a prototype contradicts a decision, update the
evidence and write a superseding decision before changing the architecture.
