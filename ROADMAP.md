# ROADMAP.md

Component-local roadmap for tatara-argo-workflows. Phase-level platform
roadmap lives in `~/Documents/tatara/ROADMAP.md`.

Statuses: `planned`, `in progress`, `shipped`.

---

## v0.1.0 - phase 5 ship

**Status:** in progress

Seven ClusterWorkflowTemplates + 3 ns-scoped Secrets in `tatara`. Onboarding
declared in infra (`events.github.repos`).

See `~/Documents/tatara/docs/superpowers/specs/2026-05-27-argo-workflows-ci-migration-design.md`.

## v0.1.1 - follow-ups

**Status:** planned

- go mod cache PVC (workflow durations: estimated 90-180s for go-ci can drop to 30s with cache)
- workflow retry-on-flake for known-flaky tests
- ARM64 builds if a target requires it
- Self-onboard tatara-argo-workflows (push_tag triggers its own helmfile-deploy via the new CWTs)
- Add tatara-tasks (phase 6) to the registry when that repo lands
