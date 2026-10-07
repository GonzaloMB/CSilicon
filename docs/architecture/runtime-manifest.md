# Runtime manifest proposal

**State:** Draft

A runtime is the complete compatibility unit, not just a Wine version.

## Required properties

- Immutable and content-addressable after publication.
- Exact component versions and SHA-256 digests.
- Trusted, allow-listed upstream sources.
- Explicit host and architecture constraints.
- Explicit Wine/DXMT integration mode and launch environment.
- Versioned prefix schema and migrations.
- Known issues and declared validation tests.
- Channel promotion by changing catalog metadata, never mutating the bundle.

## Illustrative schema

```toml
schema_version = 1
id = "candidate-001"
channel = "candidate"
published_at = "YYYY-MM-DDTHH:MM:SSZ"

[host]
architecture = "arm64"
minimum_macos = "TBD-by-research"
maximum_macos = ""
chip_families = ["TBD-by-validation"]

[wine]
version = "TBD"
source = "trusted-source-id"
url = "resolved-only-from-trusted-catalog"
sha256 = "64-lowercase-hex-characters"

[dxmt]
version = "TBD"
source = "trusted-source-id"
url = "resolved-only-from-trusted-catalog"
sha256 = "64-lowercase-hex-characters"
integration = "builtin-or-native-to-be-decided"

[prefix]
schema_version = 1
template_sha256 = "64-lowercase-hex-characters"

[launch]
executable = "validated-relative-path"
arguments = []

[compatibility]
steam_app_id = 730
cs2_build = "observed-or-range-to-be-decided"
online_policy = "unsupported-until-validated"

[[validation]]
id = "wine-smoke"
required = true

[[validation]]
id = "dx11-smoke"
required = true
```

The format must not contain credentials. Launch environment values need an
allow-list; a manifest cannot introduce arbitrary commands, dynamic scripts,
or new download authorities.

## Lifecycle

1. Resolve a manifest from a trusted catalog.
2. Validate schema and host constraints.
3. Download to a unique staging directory.
4. Verify digest and, when available, manifest/artifact signature.
5. Unpack with traversal and symlink protections.
6. Validate executable architectures and expected file inventory.
7. Run declared smoke tests.
8. Atomically activate by runtime ID.
9. Retain the previous runtime until health is confirmed.
10. Promote `candidate` to `stable` by catalog decision, not auto-update.
