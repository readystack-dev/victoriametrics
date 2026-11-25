# VictoriaMetrics: ReadyStack build kit

The offline build kit for the Docker image `readystack/victoriametrics:v1.156.0-CE-ubuntu24.04-r2`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v1.156.0-CE-ubuntu24.04-r2](https://github.com/readystack-dev/victoriametrics/releases/tag/v1.156.0-CE-ubuntu24.04-r2)
- Image: [`docker.io/readystack/victoriametrics:v1.156.0-CE-ubuntu24.04-r2`](https://hub.docker.com/r/readystack/victoriametrics/tags), manifest digest `sha256:7fc267e3a5ff591fb1218fcf2537797bb24a2cde3b27ef259be0fa34b1aa78b4`
- Product page: https://readystack.dev/products/victoriametrics
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=victoriametrics

VictoriaMetrics is distributed under its upstream licence (Apache-2.0); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [v1.156.0-CE-ubuntu24.04-r2 release](https://github.com/readystack-dev/victoriametrics/releases/tag/v1.156.0-CE-ubuntu24.04-r2): `ReadyStack-victoriametrics-v1.156.0-CE-ubuntu24.04-r2.tar.gz` (543.1 MB), SHA-256 `44b0d4215ed1761de337c8ec99a510543629d15ca3cbfe9b8d3c59c67b3d86a7`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-victoriametrics-v1.156.0-CE-ubuntu24.04-r2.rebuild.json.sigstore ReadyStack-victoriametrics-v1.156.0-CE-ubuntu24.04-r2.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-victoriametrics-v1.156.0-CE-ubuntu24.04-r2.tar.gz
cd v1.156.0-CE-ubuntu24.04-r2
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-victoriametrics-v1.156.0-CE-ubuntu24.04-r2.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/victoriametrics/recipe. The complete kit is the release download. Each release is a tag here.
