# Experiment protocol

**State:** Proposed

## Safety rules

1. Use only a CSilicon-owned prefix and directories.
2. Never modify system Wine, an existing CrossOver bottle, or a user's normal
   Steam installation.
3. Never record credentials, session cookies, API keys, or full environment
   dumps.
4. Do not attach a debugger, inject a DLL, patch CS2, or inspect game memory.
5. Begin with offline/insecure execution. Secure matchmaking is a separately
   approved research step, not part of basic launch validation.
6. Verify every downloaded artifact before execution.
7. Make setup changes reversible and record the rollback result.
8. Never disable or bypass platform or device security controls to make a test
   pass.
9. Obtain explicit approval before an application/runtime installation or
   system-level change.

## Test progression

| Stage | Test | User impact | Pass condition |
|---|---|---|---|
| E0 | Read-only host inventory | None | support facts captured and sanitized |
| E1 | Wine console smoke test | isolated prefix | deterministic executable exits correctly |
| E2 | DX11/DXMT smoke test | isolated prefix | expected image plus clean shutdown/logs |
| E3 | Steam bootstrap | login required | client starts without leaked credentials |
| E4 | CS2 offline/insecure launch | game files and disk use | menu/test scene works twice from clean state |
| E5 | Recovery test | intentionally failed activation | prior runtime remains usable |
| E6 | Performance characterization | sustained load | repeatable results with variance reported |
| E7 | Secure online evaluation | account/VAC risk | only after explicit policy and user consent |

## Experiment record template

```yaml
experiment_id: exp_YYYYMMDD_NNN
date: YYYY-MM-DD
hypothesis: ""
evidence_grade: reproduced
host:
  model: ""
  chip: ""
  macos_version: ""
  macos_build: ""
runtime:
  manifest_id: ""
  manifest_sha256: ""
procedure: []
expected: ""
observed: ""
result: pass | fail | inconclusive
run_ids: []
artifacts: []
sanitization_checked: false
follow_ups: []
```

## Reproduction threshold

A configuration becomes a candidate only after two successful runs from a
clean prefix on one host. It becomes stable only after the release gates are
met across the declared support matrix. One successful personal setup is never
called stable.
