# tatara-argo-workflows

Argo Workflows CI/CD substrate for the tatara platform.

Ships ClusterWorkflowTemplates and ns-scoped Secrets in `tatara` namespace.
Onboarding is registry-driven from the infra repo (`events.github.repos`).

See `ARCHITECTURE.md` for flow diagrams and the spec at
`~/Documents/tatara/docs/superpowers/specs/2026-05-27-argo-workflows-ci-migration-design.md`.

## Deploy

```bash
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
