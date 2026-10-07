# Vision and scope

**State:** Proposed

## Product statement

CSilicon is a local-first compatibility, runtime-management, and diagnostics
toolkit for running Counter-Strike 2 on Apple Silicon Macs through a controlled
Wine and Direct3D-to-Metal stack.

Its value is not “install the newest Wine.” Its value is turning a fragile set
of components and settings into an observable and reversible runtime whose
exact composition can be reproduced.

## Goals

- Detect whether a Mac is capable of running a supported CSilicon runtime.
- Install and validate isolated, version-pinned runtime bundles.
- Launch and stop Steam/CS2 without modifying game binaries.
- Support ordinary CS2 online play and matchmaking when the unmodified runtime
  is accepted by Steam/VAC; report a hard limitation if this cannot be proven.
- Capture enough structured evidence to explain failures and compare runs.
- Roll back every CSilicon-managed configuration change.
- Keep all normal operation local and useful without cloud services or AI.

## Non-goals

- Reimplement Wine, DXMT, Steam, or Counter-Strike 2.
- Patch, inject into, hook, or inspect CS2 process memory.
- Bypass VAC, Steam authentication, DRM, or platform restrictions.
- Promise official Valve, CodeWeavers, Wine, or DXMT support.
- Support FACEIT Anti-cheat through Wine. FACEIT currently requires Windows
  10/11, Secure Boot, and TPM 2.0 and publishes no macOS or Linux version.
- Tune gameplay, aim, network packets, or competitive behavior.
- Start with a web UI, Electron, microservices, or a cloud backend.
- Give an LLM unrestricted shell, filesystem, or network access.

## Users

The initial user is a technically capable Apple Silicon Mac owner who wants the
complete game, including online matchmaking, and accepts that this is an
unsupported compatibility path. The user may share a sanitized diagnostic
bundle manually when seeking help.

## Success criteria

The first meaningful success is not frame rate. It is repeatability:

1. The same host plus the same runtime manifest yields the same installed
   components and launch configuration.
2. Failed setup never destroys an existing working runtime.
3. Every run can be identified and its relevant environment reconstructed.
4. Diagnostic export contains no known secret or direct personal identifier.

## Safety boundary

Compatibility work remains outside the CS2 executable: Wine configuration,
DXMT configuration, prefix contents, environment, process lifecycle, and
external logs. Secure matchmaking is a separate validation surface controlled
ultimately by Valve; CSilicon cannot certify VAC safety.
