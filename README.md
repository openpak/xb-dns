# xb-dns

Original Xbox discovery DNS for OpenPak: answers only the six Xbox authentication names (as/macs/tgs) with the xb-auth address. Binds loopback high port 5353; the established OpenPak resolver forwards to it. It never binds public :53 and is not a recursive resolver. Health: `GET /healthz` on `XBDNS_HEALTH` (default 127.0.0.1:5354), `xb-dns healthcheck`. Configuration: `deploy/xb-dns.env.example` (`XBDNS_AUTH_IP`, `XBDNS_TABLE_FILE`, `XBDNS_RATE`, `XBDNS_BURST`).

## Repository

- Module `github.com/openpak/xb-dns`, image `ghcr.io/openpak/xb-dns` (static, scratch, uid 10001).
- Shared packages: `github.com/openpak/xb-common` (private; see its README for access). Service map: workspace docs `xbox/native-service-architecture.md`.
- Build and test: `GOWORK=off go build ./... && go vet ./... && go test -race ./...` (with `GOPRIVATE=github.com/openpak/*` and `gh auth setup-git`).
- Image: `podman build --secret id=netrc,src=$HOME/.netrc -t ghcr.io/openpak/xb-dns:dev .`
- Release: push a `vX.Y.Z` tag; `.github/workflows/release.yml` (tags and manual dispatch only) tests and publishes the multi-arch image. CI reads xb-common with the job's `GITHUB_TOKEN` through a netrc build secret; nothing secret is in git or in the image.
- `deploy/` holds the env example and a Podman quadlet example (digests in it are examples; production pins its own).
- Provenance and licence: AGPL-3.0-only, see `LICENSE` and `NOTICE`. Derived from the Xombie project in part; the legacy Rust workspace remains in https://github.com/openpak/xbox-live.
