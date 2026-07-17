# helm-guard

51 checks for Helm chart supply chain security. Scans Chart.yaml, values.yaml, and template files.

**Full documentation:** [ugiordan.github.io/helm-guard](https://ugiordan.github.io/helm-guard/)

**Repository:** [github.com/ugiordan/helm-guard](https://github.com/ugiordan/helm-guard)

## Check categories

| Category | Checks | Examples |
|----------|--------|---------|
| Pinning | 6 | SemVer ranges, Chart.lock, image tags, mutable values tag |
| Injection | 9 | tpl, lookup, env, getHostByName, sprig fs probes |
| Trust | 7 | Secrets, untrusted repos, hostNetwork |
| Security | 15 | CVEs, wildcard RBAC, hostPath, capabilities, runAsNonRoot, scaffolding names |
| OLM | 4 | Auto-approval, community catalog |
| + 5 more categories | 10 | Hooks, provenance, namespace, deps |
