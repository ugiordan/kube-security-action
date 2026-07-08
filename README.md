# kube-security-action

Unified GitHub Action for Kubernetes security scanning. Auto-detects repo content and runs the right tools, no configuration needed.

Wraps [tekton-guard](https://github.com/ugiordan/tekton-guard) and [helm-guard](https://github.com/ugiordan/helm-guard) into a single action with SARIF upload to GitHub Code Scanning.

## Demo

```
=== Security Scan Summary ===
tekton-guard: 4
helm-guard: 2
Total: 6

[HIGH] TKN-PIN-001: Mutable pipeline revision
  File: .tekton/push.yaml:48
  PipelineRun references pipeline with mutable revision 'main'

[CRITICAL] HLM-INJ-001: tpl function usage in templates
  File: templates/deployment.yaml:42
  Template uses tpl function enabling arbitrary template code execution
```

## Documentation

Full documentation at [ugiordan.github.io/kube-security-action](https://ugiordan.github.io/kube-security-action/)

## What gets scanned

| Tool | Target | Checks | What it catches |
|------|--------|--------|-----------------|
| [tekton-guard](https://github.com/ugiordan/tekton-guard) | `.tekton/` pipeline definitions | 48 checks, 12 categories | Mutable refs, injection, privilege escalation, trigger security, pipeline logic manipulation |
| [helm-guard](https://github.com/ugiordan/helm-guard) | `Chart.yaml`, `values.yaml`, templates | 37 checks, 10 categories | Dependency pinning, tpl injection, OLM security, CVE-based risks, chart provenance |

85 combined checks. Auto-detection runs only the tools relevant to your repo.

## Quick start

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

That's it. The action detects `.tekton/` directories and `Chart.yaml` files automatically and uploads SARIF results to GitHub Code Scanning.

## Configuration

```yaml
- uses: ugiordan/kube-security-action@v1
  with:
    fail-on: HIGH                      # Minimum severity to fail on (default: HIGH)
    format: sarif                      # Output format: json, sarif, text (default: sarif)
    tools: auto                        # Tools to run: auto, tekton-guard, helm-guard, all (default: auto)
    config-tekton: .tekton-guard.yaml  # Config file for tekton-guard (optional)
    config-helm: .helm-guard.yaml      # Config file for helm-guard (optional)
    upload-sarif: true                 # Upload SARIF to GitHub Code Scanning (default: true)
```

### Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `fail-on` | Minimum severity to fail on (`INFO`, `LOW`, `MEDIUM`, `HIGH`, `CRITICAL`) | `HIGH` |
| `format` | Output format (`json`, `sarif`, `text`) | `sarif` |
| `tools` | Which tools to run (`auto`, `tekton-guard`, `helm-guard`, `all`) | `auto` |
| `config-tekton` | Path to `.tekton-guard.yaml` config file | |
| `config-helm` | Path to `.helm-guard.yaml` config file | |
| `upload-sarif` | Upload SARIF results to GitHub Code Scanning | `true` |

### Outputs

| Output | Description |
|--------|-------------|
| `tekton-findings` | Number of tekton-guard findings |
| `helm-findings` | Number of helm-guard findings |
| `total-findings` | Total findings across all tools |

## Run specific tools

```yaml
# Only tekton-guard
- uses: ugiordan/kube-security-action@v1
  with:
    tools: tekton-guard

# Only helm-guard
- uses: ugiordan/kube-security-action@v1
  with:
    tools: helm-guard
```

## Use outputs in workflow

```yaml
- uses: ugiordan/kube-security-action@v1
  id: scan
- run: echo "Found ${{ steps.scan.outputs.total-findings }} security issues"
```

## Complete security scanning

For full coverage including RBAC privilege chain analysis, add [kube-chainsaw](https://github.com/ugiordan/kube-chainsaw) as a second step:

```yaml
- uses: ugiordan/kube-security-action@v1   # Tekton + Helm
- uses: ugiordan/kube-chainsaw@v1           # RBAC chains
  with:
    paths: config/ deploy/
```

## Tools

| Tool | Repository | Docs | Checks |
|------|------------|------|--------|
| tekton-guard | [ugiordan/tekton-guard](https://github.com/ugiordan/tekton-guard) | [Docs](https://ugiordan.github.io/tekton-guard/) | 50 |
| helm-guard | [ugiordan/helm-guard](https://github.com/ugiordan/helm-guard) | [Docs](https://ugiordan.github.io/helm-guard/) | 40 |
| kube-chainsaw | [ugiordan/kube-chainsaw](https://github.com/ugiordan/kube-chainsaw) | [Docs](https://ugiordan.github.io/kube-chainsaw/) | graph-based |

## License

Apache 2.0
