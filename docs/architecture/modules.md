# Provisional module map

**State:** Draft

The module names are conceptual. They become Rust paths only after Phase 2.

| Module | Responsibility | Must not own |
|---|---|---|
| `cli` | parse commands, render output, confirmations | platform detection or business rules |
| `application` | orchestrate use cases and transactions | raw macOS calls |
| `domain` | typed IDs, states, policies, errors, ports | filesystem/process implementation |
| `host` | normalized hardware, OS, Rosetta/translation, disk facts | runtime installation |
| `runtime` | catalog, manifest validation, staging, activation, rollback | arbitrary URLs |
| `prefix` | create, validate, migrate, snapshot CSilicon prefixes | user/system Wine prefixes |
| `process` | spawn, supervise, stop, time out, collect exit status | diagnosis conclusions |
| `launch` | construct validated Steam/CS2 launch plans | untyped shell strings |
| `diagnostics` | checks, findings, severity, remediation references | automatic destructive repair |
| `events` | structured event model, sinks, run lifecycle | secrets or raw env dumps |
| `redaction` | sanitize paths, IDs, tokens, and exports | network upload |
| `artifacts` | trusted sources, download, digest/signature, unpack | activation policy |
| `storage` | atomic files; later SQLite repositories | domain decisions |
| `platform::macos` | sysctl, processes, filesystem conventions, Keychain adapter | cross-platform policy |
| `capabilities` | future typed operations exposed to UI/AI | unrestricted shell |

## Initial command-to-module mapping

| Command | Main use case | Writes state? |
|---|---|---|
| `csilicon info` | display normalized host and app information | no |
| `csilicon doctor` | execute checks and render findings | no by default |
| `csilicon setup` | stage, verify, validate, activate runtime/prefix | yes, confirmed |
| `csilicon run` | create run record and supervise Steam/CS2 | run logs only |
| `csilicon stop` | terminate only the owned process tree | process state |
| `csilicon logs` | query/render/export sanitized run events | export only if asked |

`doctor --fix` should not exist until fixes are individually typed,
previewable, reversible, and covered by explicit confirmation policy.

## Suggested initial source layout

```text
src/
├── main.rs
├── lib.rs
├── cli/
├── application/
├── domain/
├── host/
├── runtime/
├── prefix/
├── process/
├── launch/
├── diagnostics/
├── events/
├── redaction/
├── artifacts/
├── storage/
└── platform/macos/
```

Split into crates only when at least one boundary needs separate compilation,
distribution, dependency isolation, or a stable public interface. A future
Tauri application is a likely reason to extract a reusable core crate.
