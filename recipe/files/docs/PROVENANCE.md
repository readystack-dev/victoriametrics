# Provenance — VictoriaMetrics (`v1.156.0-CE-ubuntu24.04-r2`)

Every item below is copied from a record in this archive; the record is named in brackets.

## Source

- Upstream repository: https://github.com/VictoriaMetrics/VictoriaMetrics
- Revision built: `v1.156.0` (commit `0c1bf87a0c9843c30566df0c0aa6593466425ac5`)
- Source tree: `cca4d13b23cd161ab98715415845e2c28c951328634649e864f192603afdb117` over 8928 files [`docs/provenance/SOURCE_TREE_HASH.json`]
- Community Edition only: enterprise code is removed or refused before the build (CE audit at acquire).

## Build

- Method: `source-rebuild-go`; base image `scratch + a chiselled Ubuntu 24.04 runtime (vendored/chisel/slices.txt, packages.tsv)`
- Compiled with `--network=none` from vendored source, dependencies and base images; BuildKit pinned to `moby/buildkit:v0.31.2` (shipped in `toolchain/`).
- SOURCE_DATE_EPOCH: `1795164635` [`SOURCE_DATE_EPOCH.txt`]
- Frozen inputs: [`docs/provenance/FREEZE_MANIFEST.json`], build recipe: [`docs/provenance/BUILD_RECIPE.json`].

## Output

- Published image: `readystack/victoriametrics:v1.156.0-CE-ubuntu24.04-r2` — index digest `sha256:1924a7a55a0227e37225529cf38306aa99e9043836c6c896e9a21a92b8aeefa7` [`docs/provenance/LOCKED_DIGEST.txt`]
- linux/amd64 image digest `sha256:7fc267e3a5ff591fb1218fcf2537797bb24a2cde3b27ef259be0fa34b1aa78b4` — reproduced from this archive before publishing [`docs/provenance/REPRO_VERIFICATION.json`].

## Attestations and signature

- SBOM + SLSA provenance attached to the image: attached: an SPDX SBOM and SLSA v1 provenance [`docs/provenance/SCOUT_VERDICT.json`]
- cosign signature by the ReadyStack release key: verified before publishing. Check it: `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/victoriametrics:v1.156.0-CE-ubuntu24.04-r2`

## Pinned inputs, and why

- 28 pinned inputs, each with where it came from, why this one, how it was checked and when it was decided: `docs/PINS.md` [`docs/provenance/PINS.json`] (upstream source 2, base and build images 3, image digests 2, dependency versions readystack sets 6, pins in the kit's dockerfiles 8, readystack's build engine 5, dependencies upstream chose 2).

## Build trail

- How this release passed through the ReadyStack harness, record by record (every chain, drive, stage, review round, defect and check, each naming the record it is copied from): `ReadyStack-victoriametrics-v1.156.0-CE-ubuntu24.04-r2.trail.json`, published beside this archive and signed with the release key (`ReadyStack-victoriametrics-v1.156.0-CE-ubuntu24.04-r2.trail.json.sigstore`), and readable at https://readystack.dev/products/victoriametrics/trail/v1.156.0-CE-ubuntu24.04-r2.

