# CrossOver reference baseline

**State:** Artifact validated; runtime experiment deferred  
**Reference version:** CrossOver 26.3.0

CrossOver is an external behavioral reference, not a component CSilicon may
copy, bundle, or redistribute. Its purpose is to establish whether the complete
Steam/CS2 workflow can function before investing in a separately distributable
runtime.

## Artifact provenance

| Property | Verified value |
|---|---|
| Vendor | CodeWeavers Inc. |
| Version | 26.3.0 |
| Bundle version | 26.3.0.39832 |
| Bundle ID | `com.codeweavers.CrossOver` |
| Official URL | `https://media.codeweavers.com/pub/crossover/cxmac/demo/crossover-26.3.0.zip` |
| ZIP SHA-256 | `8688e0848c4e5f79f1cc351cb52d32447da00c6c00cfd3b4bb2d164d44589a26` |
| Signing identity | `Developer ID Application: CodeWeavers Inc.` |
| Apple Team ID | `9C6B7X7Z8E` |
| Notarization | Stapled; accepted by Gatekeeper |

The checksum matches the Homebrew cask declaration, which points directly to
the CodeWeavers distribution domain. macOS validates both architecture slices
and reports that the bundle satisfies its designated requirement.

## Constraints

- The reference is a 14-day trial unless the user supplies a valid license.
- Trial activation requires explicit user confirmation.
- CSilicon does not automate purchase, registration, or credential entry.
- No CrossOver file is committed to the repository or used as a redistributable
  CSilicon dependency.
- Steam credentials are entered by the user and never captured in research
  logs or automation.

## Experiment disposition

An initial setup attempt was canceled before Steam authentication or any CS2
download. The temporary application, bottle, installer cache, and associated
local data were removed. This attempt validates artifact provenance only; it
does not provide evidence that Steam, CS2, or secure matchmaking works.

## Planned checks

1. On a dedicated test host, activate the trial and create a dedicated CS2
   bottle.
2. Install Steam from the recipe presented by CrossOver.
3. Let the user complete Steam authentication privately.
4. Install CS2 and verify its files through Steam.
5. Run offline/insecure launch and shutdown tests.
6. Evaluate normal Valve matchmaking/Premier as a separate gate.

## Primary sources

- [Official CrossOver trial download](https://www.codeweavers.com/crossover/download-links/)
- [CrossOver changelog](https://www.codeweavers.com/crossover/changelog/)
- [Homebrew cask declaration](https://github.com/Homebrew/homebrew-cask/blob/HEAD/Casks/c/crossover.rb)
