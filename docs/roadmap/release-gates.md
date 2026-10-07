# Release gates

**State:** Draft

## Gate A — `doctor` preview

- Read-only by default and useful without Wine/Steam/CS2 installed.
- Hardware and OS results are normalized and covered by fixture tests.
- No full environment dump or personal path appears in normal output.
- Unsupported/unknown is distinct from broken.

## Gate B — setup preview

- Artifact source, license, version, digest, and provenance are documented.
- Downloads cannot execute before integrity validation.
- Archive extraction rejects path traversal and unsafe links.
- Activation is atomic; rollback is tested during forced interruption.
- Existing system Wine and user prefixes remain untouched.

## Gate C — run preview

- Launch is reproduced twice from a clean prefix on every claimed host class.
- Stop targets only the process tree started by CSilicon.
- Runtime ID, config digest, host snapshot, timings, and exit outcome are saved.
- Offline/insecure behavior is labeled separately from online/VAC behavior.

## Gate D — diagnostics preview

- Structured logs have schema/version compatibility tests.
- Redaction tests cover username/home path, email, Steam identifiers, tokens,
  cookies, URLs with secrets, and environment variables.
- A user previews a bundle before export; upload never happens by default.
- Diagnostic advice cites evidence and does not claim certainty it lacks.

## Gate E — stable runtime

- Exact host support matrix is published.
- Runtime is immutable, verified, rollback-tested, and retained by ID.
- Known regressions and online/VAC policy are visible before setup.
- No critical security, privacy, licensing, or data-loss blocker remains.
- Updating is opt-in and never replaces the last working runtime silently.

## Gate F — AI advisor

- Non-AI diagnosis and all core workflows are already stable.
- The advisor receives sanitized, least-privilege inputs.
- Available operations are typed capabilities with policy checks.
- It cannot execute arbitrary shell, add download sources, access secrets, or
  perform modifying actions without explicit confirmation.
