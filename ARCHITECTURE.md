# Architecture

## CI flow (push or pull_request)

```
github push -> events.szymonrichert.pl/push -> argo-events EventSource (infra)
              -> EventBus default (NATS) -> generic Sensor (infra)
              -> Workflow submission in tatara ns from CWT tatara-go-ci
              -> report-pending -> clone -> golangci-lint -> go test -race
              -> onExit -> tatara-github-status -> github commit status
```

Single status check: `tatara/ci`.

## Release flow (tag push on tatara-cli)

Same trigger lane, dispatches to CWT `tatara-go-release`. Steps:
report-pending -> clone (full) -> goreleaser -> onExit.

goreleaser handles: amd64 binary tarball, github release upload, container
push to harbor.

Single status check: `tatara/release`.

## Tag flow on tatara-memory (composite)

Dispatches to CWT `tatara-memory-tag`. DAG:

```
container-build -+
                  +-> helmfile-deploy
helm-publish ----+
```

Four status checks: `tatara/container`, `tatara/chart`, `tatara/deploy`,
`tatara/tag-pipeline` (aggregate).

## Status reporting

Every atomic CWT runs `tatara-github-status` as a first step (state=pending)
and again via `onExit` (state=success|failure|error mapped from
`{{workflow.status}}`). The composite CWT also reports its aggregate state.

PAT `github-status-token` (scope `repo:status` + `contents:write`) lives in
ns Secret `github-status-token` keyed `GITHUB_TOKEN`.
