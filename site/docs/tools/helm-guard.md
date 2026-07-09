# helm-guard

42 checks for Helm chart supply chain security. Scans Chart.yaml, values.yaml, and template files.

**Full documentation:** [ugiordan.github.io/helm-guard](https://ugiordan.github.io/helm-guard/)

**Repository:** [github.com/ugiordan/helm-guard](https://github.com/ugiordan/helm-guard)

## Check categories

| Category | Checks | Examples |
|----------|--------|---------|
| Pinning | 5 | SemVer ranges, Chart.lock, image tags |
| Injection | 8 | tpl, lookup, env, getHostByName |
| Trust | 7 | Secrets, untrusted repos, hostNetwork |
| Security | 6 | Path traversal CVEs, symlink, SA automount |
| OLM | 4 | Auto-approval, community catalog |
| + 5 more categories | 12 | Hooks, provenance, namespace, deps |
