# Action Outputs

| Output | Description |
|--------|-------------|
| `tekton-findings` | Number of tekton-guard findings |
| `helm-findings` | Number of helm-guard findings |
| `total-findings` | Total findings across all tools |

## Using outputs

```yaml
      - uses: ugiordan/kube-security-action@v1
        id: scan

      - name: Check results
        if: steps.scan.outputs.total-findings != '0'
        run: echo "Found ${{ steps.scan.outputs.total-findings }} security issues"
```
