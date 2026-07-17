# Quick Start

## Basic Usage

Add to `.github/workflows/security-scan.yml`:

```yaml
name: Security Scan
on:
  push:
    branches: [main]
  pull_request:

permissions:
  security-events: write

jobs:
  scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: ugiordan/kube-security-action@v1
```

## What happens

1. The action checks out your code
2. Installs tekton-guard and helm-guard
3. Auto-detects `.tekton/` dirs and `Chart.yaml` files
4. Runs the appropriate scanner(s)
5. Uploads SARIF to GitHub Code Scanning
6. Reports finding counts

## Fail on severity

```yaml
      - uses: ugiordan/kube-security-action@v1
        with:
          fail-on: HIGH  # Only fail on HIGH+ findings
```

## Text output (no SARIF)

```yaml
      - uses: ugiordan/kube-security-action@v1
        with:
          format: text
          upload-sarif: 'false'
```

---

## Complete security scanning setup

For full coverage including RBAC privilege chain analysis, add [kube-chainsaw](https://github.com/ugiordan/kube-chainsaw) as a second step:

```yaml
name: Security Scan
on: [push, pull_request]

permissions:
  security-events: write

jobs:
  scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      # Tekton + Helm security (auto-detected)
      - uses: ugiordan/kube-security-action@v1

      # RBAC privilege chain analysis
      - uses: ugiordan/kube-chainsaw@v1
        with:
          paths: config/ deploy/
          fail-on: HIGH
```

| Step | Tool | What it scans | Checks |
|------|------|---------------|--------|
| 1 | kube-security-action | `.tekton/` + `Chart.yaml` | 111 (60 + 51) |
| 2 | kube-chainsaw | RBAC manifests | graph-based |
