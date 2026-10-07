# Research backlog

**State:** Draft

Priority is ordered by what can invalidate the product earliest.

## P0 — feasibility blockers

- [ ] Define sanitized host-inventory fields and test them on representative
  Apple Silicon fixtures without committing data from personal machines.
- [x] Compare macOS, Linux VM, and bare-metal Linux at the architectural level.
- [ ] Install/test CrossOver 26.3 only after separate explicit approval and use
  it as a reference baseline; do not redistribute or inspect proprietary
  components.
- [ ] Identify a candidate Wine build whose architecture and exported macOS
  driver APIs satisfy the selected DXMT build.
- [ ] Record upstream source, version/commit, license, signature/checksum, and
  build provenance for every artifact.
- [ ] Run a non-Steam 64-bit Windows smoke executable under the isolated Wine
  prefix.
- [ ] Run a deterministic Direct3D 11 smoke executable through DXMT and capture
  logs without game-process injection.
- [ ] Install/bootstrap Steam in the isolated prefix without storing or logging
  credentials.
- [ ] Launch CS2 offline or in explicitly insecure mode and record rendering,
  input, audio, process tree, and shutdown behavior.
- [ ] Test VAC-secure matchmaking only after the offline baseline and integrity
  checks pass, with explicit user consent and an account-risk warning.
- [ ] Establish a written VAC/secure matchmaking policy. Full online play is a
  product requirement; if unsupported, that is a feasibility blocker rather
  than a feature to defer silently.

## P1 — architecture inputs

- [ ] Compare bundled upstream Wine, a CSilicon-built Wine, and an explicitly
  user-selected external runtime for supportability and licensing.
- [ ] Decide whether DXMT uses Wine built-ins or prefix-level native DLL
  overrides, then document validation rules.
- [ ] Define runtime compatibility fields for macOS builds, chip families,
  Wine/DXMT coupling, Steam client state, and CS2 build/channel.
- [ ] Catalogue logs available from Wine, DXMT, macOS unified logging, process
  exit status, and crash reports.
- [ ] Test the redactor against usernames, home paths, emails, Steam IDs,
  access tokens, cookies, and arbitrary environment secrets.
- [ ] Determine whether early run history justifies SQLite or whether atomic
  JSON event files are sufficient.
- [ ] Define disk usage and cleanup rules for runtimes, prefixes, Steam/CS2,
  shader caches, logs, and diagnostic bundles.

## P2 — productization

- [ ] Define signing, notarization, Gatekeeper, quarantine, and update behavior.
- [ ] Define manifest signing and trusted-key rotation.
- [ ] Design atomic runtime activation and rollback under interruption.
- [ ] Measure cold/warm launch, frame pacing, input latency, memory pressure,
  and shader-cache behavior with a reproducible test scene.
- [ ] Validate more than one Apple Silicon generation before claiming broad
  device support.
- [ ] Write upstream contribution boundaries for Wine/DXMT fixes.

## Explicitly deferred

- Tauri/React UI.
- AI diagnosis or provider integrations.
- Automated optimization.
- Cloud sync, telemetry, accounts, or a hosted backend.
- Any secure-matchmaking claim before the P0 policy is resolved.
