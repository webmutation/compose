# Security Patches

## CVE Patches Applied on 2026-03-27

This document describes the security vulnerabilities patched in this fork of
[docker/compose](https://github.com/docker/compose) (based on v5.1.1).

### Patched CVEs

| Severity | CVE | Package | Fixed In |
|----------|-----|---------|----------|
| HIGH | [CVE-2025-47913](https://pkg.go.dev/vuln/GO-2025-3751) | `golang.org/x/crypto` | v0.49.0 |
| MEDIUM | [CVE-2025-58181](https://pkg.go.dev/vuln/GO-2025-3804) | `golang.org/x/crypto` | v0.49.0 |
| MEDIUM | [CVE-2025-47914](https://pkg.go.dev/vuln/GO-2025-3752) | `golang.org/x/crypto` | v0.49.0 |
| HIGH | [CVE-2024-25621](https://pkg.go.dev/vuln/GO-2024-2598) | `github.com/containerd/containerd/v2` | v2.2.2 |
| MEDIUM | [CVE-2025-64329](https://pkg.go.dev/vuln/GO-2025-3840) | `github.com/containerd/containerd/v2` | v2.2.2 |

### Versions Updated

| Package | Before | After |
|---------|--------|-------|
| `golang.org/x/crypto` | v0.48.0 | v0.49.0 |
| `github.com/containerd/containerd/v2` | v2.2.2 | v2.2.2 (latest available) |

### How to Build the Patched Binary

Requirements: Go 1.23+, Docker Engine 20.10+, `make`

```bash
# Clone the fork
git clone https://github.com/webmutation/compose.git
cd compose
git checkout fix/cve-patches

# Build the binary
make

# The patched binary is output at:
./bin/build/docker-compose
```

To install as a Docker CLI plugin:

```bash
mkdir -p ~/.docker/cli-plugins
cp ./bin/build/docker-compose ~/.docker/cli-plugins/docker-compose
chmod +x ~/.docker/cli-plugins/docker-compose

# Verify
docker compose version
```

### Vulnerability Scanning

To re-scan for vulnerabilities after building:

```bash
go install golang.org/x/vuln/cmd/govulncheck@latest
govulncheck ./...
```

A `govulncheck` step has been added to the CI workflow (`.github/workflows/ci.yml`)
to automatically prevent future vulnerable dependency regressions on every PR.
