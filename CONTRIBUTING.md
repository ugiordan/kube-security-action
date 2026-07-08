# Contributing to kube-security-action

Thanks for your interest in contributing!

## How It Works

This is a composite GitHub Action that wraps [tekton-guard](https://github.com/ugiordan/tekton-guard) and [helm-guard](https://github.com/ugiordan/helm-guard). Most security check improvements should go to those repos, not this one.

## When to Contribute Here

- Changes to the auto-detection logic
- New tool integrations
- Action input/output changes
- Documentation improvements

## Development

The action is defined in `action.yml`. Test changes by referencing your fork in a workflow:

```yaml
- uses: your-fork/kube-security-action@your-branch
```

## Pull Requests

- Test the action in a real workflow before submitting
- Update README.md and docs if changing inputs/outputs

## License

Apache 2.0
