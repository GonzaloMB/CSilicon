# Delivery phases

**State:** Proposed

Phases are evidence gates, not calendar promises. Later phases do not begin
because an earlier prototype “mostly works.”

## Phase 0 — product framing (complete)

**Outputs:** vision, boundaries, safety principles, initial ADRs.  
**Gate:** scope distinguishes compatibility tooling from game modification.

## Phase 1 — technical feasibility (active)

**Outputs:** reproducible experiments, compatibility matrix, licensing report,
diagnostic sources, online/VAC policy, validated risks.  
**Gate:** all exit criteria in [the research plan](../research/README.md).

## Phase 2 — detailed architecture

**Outputs:** accepted module boundaries, domain model, manifest schema, threat
model, storage decision, error taxonomy, CLI contract, test strategy.  
**Gate:** every modifying workflow has validation, confirmation, rollback, and
failure semantics.

## Phase 3 — Milestone 0: inspect

**Commands:** `csilicon info`, `csilicon doctor`.  
**Scope:** read-only host/environment detection; no runtime installation.  
**Gate:** golden outputs, unit tests, real-hardware tests, privacy review.

## Phase 4 — Milestone 1: setup

**Command:** `csilicon setup`.  
**Scope:** trusted catalog, download, checksum/signature, staging, validation,
isolated prefix, atomic activation, rollback.  
**Gate:** clean setup and interrupted/failed setup are reproducible.

## Phase 5 — Milestone 2: run

**Commands:** `csilicon run`, `csilicon stop`.  
**Scope:** launch plans, owned process tree, run IDs, offline/insecure baseline,
clean and forced shutdown.  
**Gate:** repeated launch on declared hosts without mutating game binaries.

## Phase 6 — Milestone 3: observe and diagnose

**Commands:** `csilicon logs`, later `csilicon diagnose`.  
**Scope:** structured events, crash/exit evidence, sanitization, diagnostic
bundle, deterministic rule-based findings.  
**Gate:** seeded failures are correctly detected and exports pass redaction.

## Phase 7 — Milestone 4: benchmark

**Command:** `csilicon benchmark`.  
**Scope:** non-injected measurements, experiment comparison, variance and host
context.  
**Gate:** method is repeatable and does not interact with secure play.

## Phase 8 — product UI

**Scope:** Tauri + React/TypeScript over the stable Rust capability layer.  
**Gate:** parity with supported CLI workflows and no duplicated business logic.

## Phase 9 — optional AI advisor

**Command:** optional `csilicon diagnose --advisor`.  
**Scope:** local or explicitly configured provider, typed read capabilities,
experiment proposals, confirmations for changes.  
**Gate:** CSilicon remains fully functional without AI, API key, or network.
