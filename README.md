# xb-dns

OpenPak's Xbox DNS Server.

| | |
| --- | --- |
| Network | Original Xbox |
| Role | Discovery DNS: exact-name answers for the six Xbox authentication names (as/macs/tgs) |
| Depends on | [`xb-common`](https://github.com/openpak/xb-common) (private) |
| Image | `ghcr.io/openpak/xb-dns` |
| Based on | [Xombie](https://github.com/XombieOnline/xombie) (AGPL-3.0), in part |
| Licence | AGPL-3.0-only |

## What it serves

| Endpoint | What |
| --- | --- |
| UDP DNS on `XBDNS_BIND` (default `127.0.0.1:5353`) | Exact-name answers for the six Xbox authentication names with the xb-auth address; not a recursive resolver |
| `GET /healthz` on `XBDNS_HEALTH` (default `127.0.0.1:5354`) | Health check; `xb-dns healthcheck` runs it |
| `GET /metrics` on `XBDNS_HEALTH` | Traffic counters only; no client address or name is kept |

## Build

```sh
GOWORK=off go build ./... && go vet ./... && go test -race ./...
```

Needs `GOPRIVATE=github.com/openpak/*` and `gh auth setup-git`. Image and release steps are in [Deploy](docs/deploy.md).

## Docs

- [Protocol](docs/protocol.md)
- [Evidence](docs/evidence.md)
- [Deploy](docs/deploy.md)
- [Notes](docs/notes.md)

## Licence

AGPL-3.0-only. See [LICENSE](LICENSE) and [NOTICE](NOTICE).
