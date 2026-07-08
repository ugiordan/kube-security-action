# Action Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `fail-on` | Minimum severity to fail on | `HIGH` |
| `format` | Output format (json, sarif, text) | `sarif` |
| `config-tekton` | Config file for tekton-guard | none |
| `config-helm` | Config file for helm-guard | none |
| `upload-sarif` | Upload SARIF to GitHub Code Scanning | `true` |
| `tools` | Which tools to run | `auto` |

## `tools` options

| Value | Behavior |
|-------|----------|
| `auto` | Detect `.tekton/` and `Chart.yaml`, run matching tools |
| `tekton-guard` | Only run tekton-guard |
| `helm-guard` | Only run helm-guard |
| `all` | Run all tools regardless of detection |
