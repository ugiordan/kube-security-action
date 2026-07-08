# kube-security-action

Unified GitHub Action for Kubernetes security scanning. Auto-detects repo content and runs the appropriate tools:

- **[tekton-guard](https://github.com/ugiordan/tekton-guard)** for `.tekton/` pipeline definitions (50 checks)
- **[helm-guard](https://github.com/ugiordan/helm-guard)** for Helm charts (40 checks)

## Usage

```yaml
name: Security Scan
on: [push, pull_request]

jobs:
  scan:
    runs-on: ubuntu-latest
    permissions:
      security-events: write
    steps:
      - uses: actions/checkout@v4
      - uses: ugiordan/kube-security-action@v1
```

### With options

```yaml
      - uses: ugiordan/kube-security-action@v1
        with:
          fail-on: HIGH
          config-tekton: .tekton-guard.yaml
          config-helm: .helm-guard.yaml
```

### Run specific tools

```yaml
      - uses: ugiordan/kube-security-action@v1
        with:
          tools: tekton-guard  # or: helm-guard, all, auto (default)
```

## Outputs

| Output | Description |
|--------|-------------|
| `tekton-findings` | Number of tekton-guard findings |
| `helm-findings` | Number of helm-guard findings |
| `total-findings` | Total findings across all tools |

## License

Apache 2.0
