# Configuration

## Config files

Create `.tekton-guard.yaml` and/or `.helm-guard.yaml` in your repo root:

```yaml
# .github/workflows/security-scan.yml
      - uses: ugiordan/kube-security-action@v1
        with:
          config-tekton: .tekton-guard.yaml
          config-helm: .helm-guard.yaml
```

See the individual tool docs for config file format:
- [tekton-guard configuration](https://ugiordan.github.io/tekton-guard/guides/configuration/)
- [helm-guard configuration](https://ugiordan.github.io/helm-guard/guides/configuration/)

## Tool selection

```yaml
      - uses: ugiordan/kube-security-action@v1
        with:
          tools: tekton-guard  # Only run tekton-guard
```

Options: `auto` (default), `tekton-guard`, `helm-guard`, `all`
