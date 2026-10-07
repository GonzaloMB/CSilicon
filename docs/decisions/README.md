# Architecture decision records

Decision records explain choices that would otherwise be rediscovered or
silently reversed.

| ADR | State | Decision |
|---|---|---|
| [0001](0001-native-macos-runtime.md) | Accepted | Runtime executes natively on macOS, without Docker |
| [0002](0002-rust-cli-first.md) | Accepted | Rust core and CLI-first delivery |
| [0003](0003-versioned-runtime-bundles.md) | Accepted | Wine/DXMT/configuration are one versioned runtime |

New decisions should record context, decision, consequences, rejected options,
and evidence. Use the next four-digit number; never rewrite the history of an
accepted decision when a superseding ADR is clearer.
