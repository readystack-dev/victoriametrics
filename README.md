[![ReadyStack](https://readystack.dev/logo.svg)](https://readystack.dev)

**Stable, Open-source Releases, Automated** · [readystack.dev](https://readystack.dev)

[![Docker Hub](https://img.shields.io/badge/Docker%20Hub-readystack%2Fvictoriametrics-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/r/readystack/victoriametrics) [![Docker pulls](https://img.shields.io/docker/pulls/readystack/victoriametrics)](https://hub.docker.com/r/readystack/victoriametrics) [![Grade at release](https://img.shields.io/badge/grade%20at%20release-A%20%2894%25%29-2ea44f)](https://readystack.dev/products/victoriametrics) [![Signed: cosign](https://img.shields.io/badge/signed-cosign-2ea44f)](https://readystack.dev/keys/cosign.pub) ![SBOM: SPDX](https://img.shields.io/badge/SBOM-SPDX-2ea44f) ![Provenance: SLSA v1](https://img.shields.io/badge/provenance-SLSA%20v1-2ea44f) ![Offline rebuild: verified](https://img.shields.io/badge/offline%20rebuild-verified-2ea44f)

# VictoriaMetrics: ReadyStack build kit

The offline build kit for the Docker image `readystack/victoriametrics:v1.156.0-CE-ubuntu24.04-r2`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v1.156.0-CE-ubuntu24.04-r2](https://github.com/readystack-dev/victoriametrics/releases/tag/v1.156.0-CE-ubuntu24.04-r2)
- Image: [`docker.io/readystack/victoriametrics:v1.156.0-CE-ubuntu24.04-r2`](https://hub.docker.com/r/readystack/victoriametrics/tags), manifest digest `sha256:7fc267e3a5ff591fb1218fcf2537797bb24a2cde3b27ef259be0fa34b1aa78b4`
- Product page: https://readystack.dev/products/victoriametrics
- Source and build recipe: https://readystack.dev/products/victoriametrics/recipe
- Build trail: https://readystack.dev/products/victoriametrics/trail/v1.156.0-CE-ubuntu24.04-r2
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=victoriametrics

## The image

ReadyStack VictoriaMetrics Community Edition build kit.

## Who uses VictoriaMetrics and why

Operations and SRE teams who store and query large volumes of monitoring metrics.

VictoriaMetrics is a time series database and monitoring solution, open source in both its single-node and cluster versions, with its own query language, MetricsQL.

A typical use: A company's monitoring has outgrown the local storage of its servers. Agents send metrics to a VictoriaMetrics cluster, which keeps them for long-term storage; dashboards query them with MetricsQL, and alert rules run against the same data.

From the upstream project's own description: https://github.com/VictoriaMetrics/VictoriaMetrics, https://docs.victoriametrics.com/.

## This release

- Docker Scout policy grade at release: **A** (94%), graded 2026-11-20 with `docker scout policy` (CLI 1.26.0, docker-default configuration).
  - Docker Scout counts 10 packages with copyleft licences (GPL, LGPL, MPL), all of them operating-system packages (it counts only packages whose licence it can read; the SBOM lists every component).
- Signed with ReadyStack's release key (fingerprint `04daa92344a52dbc`): https://readystack.dev/keys/cosign.pub.
- Runs as a non-root user (`victoriametrics`).
- Attestations on the image: an SPDX SBOM and SLSA provenance v1.
- Rebuilt from this kit with network egress blocked on 2026-11-20; the rebuilt image digest is the published one.
- Base: Ubuntu 24.04.

The current grade, measured again every day, is on https://readystack.dev/products/victoriametrics.

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

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/victoriametrics/recipe. The complete kit is the release download. Each release is a tag here. How to report a vulnerability: [SECURITY.md](SECURITY.md).

## About ReadyStack

**Stable, Open-source Releases, Automated.** ReadyStack releases popular open-source apps every week with every available critical and high security fix applied, plus full documentation, reference data, tests and a build recipe that recreates each release bit-for-bit. Each release is rebuilt from its pinned inputs with the network off, checked against its published digest, signed, and scanned and graded again every day. The images and build kits are free, and ReadyStack is soon to be a nonprofit.

[readystack.dev](https://readystack.dev) · [All products](https://readystack.dev/products.html) · [Build kits on GitHub](https://github.com/readystack-dev) · [Defect log](https://readystack.dev/defects.html) · contact@readystack.dev

— ReadyStack · https://readystack.dev
