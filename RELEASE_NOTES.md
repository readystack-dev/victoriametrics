# VictoriaMetrics v1.156.0 — ReadyStack release `v1.156.0-CE-ubuntu24.04-r2`

Generated 2026-11-20 from this release's build records and strategy. Statements that come from a single record name it in brackets; the others come from this release's strategy and build log.

## Release

- **Image:** `readystack/victoriametrics:v1.156.0-CE-ubuntu24.04-r2` (linux/amd64). Index digest `sha256:1924a7a55a0227e37225529cf38306aa99e9043836c6c896e9a21a92b8aeefa7` [`docs/provenance/LOCKED_DIGEST.txt`].
- **Image manifest digest:** `sha256:7fc267e3a5ff591fb1218fcf2537797bb24a2cde3b27ef259be0fa34b1aa78b4` [`TARGET_DIGEST.txt`].
- **Upstream:** VictoriaMetrics v1.156.0 built from source at `v1.156.0` of https://github.com/VictoriaMetrics/VictoriaMetrics — upstream notes: https://github.com/VictoriaMetrics/VictoriaMetrics/releases/tag/v1.156.0 [`docs/provenance/BUILD_RECIPE.json`].
- **Base image:** none (`FROM scratch`): a chiselled Ubuntu 24.04 runtime, the files Canonical's chisel cut from Ubuntu's own packages (`vendored/chisel/slices.txt`, `vendored/chisel/packages.tsv`); runtime user `victoriametrics`.
- **Build:** `source-rebuild-go`, compiled offline with `--network=none`.
- **Supersedes:** ReadyStack release `v1.156.0-CE-ubuntu24.04-r1`.

## What changed in this release

- Upstream version unchanged (v1.156.0); ReadyStack rebuild.
- Minimum dependency versions ReadyStack enforces on top of upstream (raised only where upstream's own version was lower); shipped versions from the SBOM [`docs/sbom/SBOM.json`]:
  - `github.com/go-jose/go-jose/v4` at least `v4.1.6`: not raised, upstream already pins `v4.1.9` (shipped: `v4.1.9`)
  - `golang.org/x/net` at least `v0.62.0`: not raised, upstream already pins `v0.62.0` (shipped: `v0.62.0`)
  - `github.com/klauspost/compress` at least `v1.20.2`: not raised, upstream already pins `v1.20.3` (shipped: `v1.20.3`)
- VictoriaMetrics v1.156.0 is unchanged from the release this supersedes (v1.156.0-CE-ubuntu24.04-r1); this release rebuilds it. Changes: the image is rebuilt on the current ubuntu:24.04 image (sha256:9c7f200c07e3…), which its maintainers updated after v1.156.0-CE-ubuntu24.04-r1 was built on sha256:2198e4c65076…. Settings, ports and data volumes are those of v1.156.0-CE-ubuntu24.04-r1: replace the container with this image on the same volumes.

## Security status at release (measured 2026-11-20)

- **Docker Scout:** 0 fixable critical/high vulnerabilities; runs as `victoriametrics` (non-root); SBOM + provenance attestations present (SPDX SBOM + SLSA v1) [`docs/provenance/SCOUT_VERDICT.json`].
- **OSV cross-check:** no fixable critical/high vulnerability beyond Docker Scout's findings.
- **Signature:** cosign signature verified by ReadyStack's release gate before publishing; check it yourself with `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/victoriametrics:v1.156.0-CE-ubuntu24.04-r2` (signatures are recorded in the public Sigstore transparency log).
- **ReadyStack release check at release:** passed (ReadyStack's own test, not a Docker Scout grade). Vulnerabilities are disclosed every day and the image never changes, so it is re-checked daily, beside Docker Scout's own dated grade, at https://readystack.dev/queue.

## Reproducibility

Rebuilds offline from this archive to the identical image digest `sha256:7fc267e3a5ff591fb1218fcf2537797bb24a2cde3b27ef259be0fa34b1aa78b4`: run `./BUILD_OFFLINE.sh`, then `./VERIFY_OFFLINE.sh` (add `--online` to confirm the Docker Hub tag holds the same digest). Before publishing, ReadyStack rebuilt the kit with `./BUILD_OFFLINE.sh` and compared the result with the published digest [`docs/provenance/REPRO_VERIFICATION.json`], then ran `./BUILD_OFFLINE.sh` and `./VERIFY_OFFLINE.sh` from this archive (without `--online`).

## Validation

- 6 of 6 use cases passed (6 authored) against the running image [`docs/validation/test-results.json`].

## Known issues

- None recorded.

## Defects fixed

- 11 problems found before release and fixed before it shipped (11 by review); each is listed in `docs/defects/defects.json`.

## Verify this archive

```
sha256sum -c CHECKSUMS.sha256
./BUILD_OFFLINE.sh && ./VERIFY_OFFLINE.sh --online
cosign verify --key https://readystack.dev/keys/cosign.pub readystack/victoriametrics:v1.156.0-CE-ubuntu24.04-r2
```

ReadyStack records every signature in the public Sigstore transparency log (Rekor), so the command needs no extra flags.

