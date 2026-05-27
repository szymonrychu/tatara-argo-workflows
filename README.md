# tatara-argo-workflows

Argo Workflows CI/CD substrate for the tatara platform.

Ships ClusterWorkflowTemplates and ns-scoped Secrets in `tatara` namespace.
Onboarding is registry-driven from the infra repo (`events.github.repos`).

This repo owns the chart only. The helm release is defined in the infra
repo (`~/Documents/infra/helmfile/`) - same separation as `argo-workflows`
and `argo-events` substrate releases. Values (including sops-encrypted
secrets) live in `~/Documents/infra/helmfile/helmfiles/coding/values/tatara-argo-workflows/`.

See `ARCHITECTURE.md` for flow diagrams and the spec at
`~/Documents/tatara/docs/superpowers/specs/2026-05-27-argo-workflows-ci-migration-design.md`.

## Deploy

From the infra helmfile directory:

```bash
cd ~/Documents/infra/helmfile/helmfiles/coding
helmfile -e default apply -l name=tatara-argo-workflows
```

## Smoke

```bash
argo submit -n tatara \
  --from clusterworkflowtemplate/tatara-go-ci \
  --parameter repo=szymonrychu/tatara-cli \
  --parameter ref=refs/heads/main \
  --parameter sha=<a-commit-sha>
```
