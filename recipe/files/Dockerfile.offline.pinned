# GENERATED L-009 hermetic build (--network=none, SBOM+SLSA-attestation-producing).
# Pinned bases from BASE_IMAGE_DIGESTS.lock; vendored Go tree + debs from Dockerfile.vendor.
FROM golang:1.27.4-bookworm@sha256:4fa7c968ba93f1635670522dbb01a2c78150443e1385746924566079f36570ea AS build_victoria-metrics
WORKDIR /src
COPY vendored/victoriametrics-src/ .
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOWORK=off GOFLAGS="-mod=vendor -buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795164635
RUN go build -trimpath -ldflags='-s -w -X github.com/VictoriaMetrics/VictoriaMetrics/lib/buildinfo.Version=victoria-metrics-20261120-085035-tags-v1.156.0-0-g0c1bf87a0c' -o /victoria-metrics ./app/victoria-metrics && /victoria-metrics -version && \
    { readelf -lW /victoria-metrics | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; readelf -dW /victoria-metrics | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; } > /victoria-metrics.needs
FROM golang:1.27.4-bookworm@sha256:4fa7c968ba93f1635670522dbb01a2c78150443e1385746924566079f36570ea AS build_vmctl
WORKDIR /src
COPY vendored/victoriametrics-src/ .
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOWORK=off GOFLAGS="-mod=vendor -buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795164635
RUN go build -trimpath -ldflags='-s -w' -o /vmctl ./app/vmctl && /vmctl --help && \
    { readelf -lW /vmctl | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; readelf -dW /vmctl | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; } > /vmctl.needs
# rs-probe: the HEALTHCHECK helper (standard library only, from the kit's rs-probe.go)
FROM golang:1.27.4-bookworm@sha256:4fa7c968ba93f1635670522dbb01a2c78150443e1385746924566079f36570ea AS build_rs_probe
WORKDIR /probe
COPY rs-probe.go main.go
COPY rs-probe.mod go.mod
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOFLAGS="-buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795164635
RUN go build -trimpath -ldflags='-s -w' -o /rs-probe .
# the chiselled rootfs (vendored/chisel, cut by Dockerfile.vendor), the service user, the binaries
FROM ubuntu:24.04@sha256:9c7f200c07e3d4a03e7249d2c16bf66a51120fb876aa2242cf31451412543289 AS rootfs
ARG SOURCE_DATE_EPOCH=1795164635
ADD vendored/chisel/rootfs.tar /rootfs/
RUN printf 'victoriametrics:x:999:999::/victoria-metrics-data:/bin/sh\n' >> /rootfs/etc/passwd && printf 'victoriametrics:x:999:\n' >> /rootfs/etc/group && \
    mkdir -p /rootfs/victoria-metrics-data && chown -R 999:999 /rootfs/victoria-metrics-data
COPY --from=build_victoria-metrics /victoria-metrics /rootfs/usr/bin/victoria-metrics
COPY --from=build_victoria-metrics /victoria-metrics.needs /tmp/needs/victoria-metrics
COPY --from=build_vmctl /vmctl /rootfs/usr/bin/vmctl
COPY --from=build_vmctl /vmctl.needs /tmp/needs/vmctl
COPY --from=build_rs_probe /rs-probe /rootfs/usr/local/bin/rs-probe
RUN chmod 755 /rootfs/usr/bin/victoria-metrics /rootfs/usr/bin/vmctl /rootfs/usr/local/bin/rs-probe
RUN --mount=type=bind,source=vendored/chisel,target=/chisel set -eu; \
    for n in /tmp/needs/*; do while read -r lib; do [ -n "$lib" ] || continue; \
      case "$lib" in /*) [ -e "/rootfs$lib" ] ;; *) [ -n "$(find /rootfs/usr/lib /rootfs/usr/lib64 -name "$lib" 2>/dev/null | head -1)" ] ;; esac || \
      { echo "$(basename "$n") needs $lib, which the chiselled rootfs does not have: add its slice to runtime_base.slices" >&2; exit 1; }; \
    done < "$n"; done; rm -rf /tmp/needs; \
    [ -e /rootfs/etc/os-release ] || { echo "no /etc/os-release: base-files_release-info is missing" >&2; exit 1; }; \
    [ "$(grep -c '^Package: ' /rootfs/var/lib/dpkg/status)" = "$(wc -l < /chisel/packages.tsv)" ] || \
      { echo "/var/lib/dpkg/status does not list every package of vendored/chisel/packages.tsv" >&2; exit 1; }; \
    rm -rf /rootfs/var/log/dpkg.log /rootfs/var/log/alternatives.log /rootfs/var/log/apt /rootfs/var/cache/ldconfig/aux-cache /rootfs/var/cache/fontconfig
FROM scratch
ARG SOURCE_DATE_EPOCH=1795164635
COPY --from=rootfs /rootfs/ /
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
LABEL org.opencontainers.image.licenses="Apache-2.0"
LABEL org.opencontainers.image.title="VictoriaMetrics"
LABEL org.opencontainers.image.source="https://github.com/VictoriaMetrics/VictoriaMetrics"
LABEL org.opencontainers.image.version="v1.156.0-CE-ubuntu24.04-r2"
LABEL org.opencontainers.image.revision="0c1bf87a0c9843c30566df0c0aa6593466425ac5"
HEALTHCHECK --interval=5s --timeout=30s --start-period=20s \
  CMD /usr/local/bin/rs-probe http://127.0.0.1:8428/health || exit 1
USER victoriametrics
EXPOSE 8428
ENTRYPOINT ["victoria-metrics", "-storageDataPath=/victoria-metrics-data", "-httpListenAddr=:8428", "-retentionPeriod=12"]
