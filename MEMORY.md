# MEMORY.md

Component-local memory for tatara-argo-workflows. Cross-repo decisions live
in `~/Documents/tatara/MEMORY.md`.

Format: `YYYY-MM-DD - decision/finding`

---

## Decisions

2026-05-27 - repo bootstrapped; ships only ClusterWorkflowTemplates + ns Secrets. EventSource, Sensor, EventBus, github HMAC secret stay in `~/Documents/infra/` argo-events release.
2026-05-27 - per-step github status (not aggregate-only) because debugging a failed tag pipeline benefits from knowing which sub-step (container/chart/deploy) failed without opening argo UI.
2026-05-27 - composite CWT for tatara-memory-tag only; tatara-cli's `.goreleaser.yaml` handles release+container in one step so push_tag dispatches directly to tatara-go-release.
2026-05-27 - buildkit-daemonless (single container, no sidecar) over kaniko because kaniko needs separate invocations for multi-arch; we're amd64-only so single-invocation either works, but buildkit's path is simpler if multi-arch is added later.

## Dead-ends / things tried that did not work

*(nothing yet)*

## Open questions

*(nothing yet)*
