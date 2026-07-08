# tekton-guard

50 checks for Tekton pipeline security. Scans PipelineRun, Pipeline, Task, StepAction, TriggerTemplate, EventListener, and Repository CRDs.

**Full documentation:** [ugiordan.github.io/tekton-guard](https://ugiordan.github.io/tekton-guard/)

**Repository:** [github.com/ugiordan/tekton-guard](https://github.com/ugiordan/tekton-guard)

## Check categories

| Category | Checks | Examples |
|----------|--------|---------|
| Pinning | 5 | Mutable refs, unpinned bundles |
| Trust | 7 | Untrusted sources, unknown resolvers |
| Triggers | 9 | CEL injection, TriggerTemplate, EventListener |
| Pipeline Logic | 7 | Finally block, onError, TOCTOU |
| Chains | 6 | VerificationPolicy, result poisoning |
| + 7 more categories | 16 | SA, workspace, injection, security, volumes, exfiltration, limits |
