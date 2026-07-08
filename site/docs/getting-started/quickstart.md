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
