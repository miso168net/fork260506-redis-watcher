# Design: Redis Watcher Retro Spec

**Date**: 2026-05-07
**Author**: brainstorming session (user: miso168net, agent: Claude Opus 4.7)
**Status**: Approved (user-confirmed 2026-05-07; transition to writing-plans intentionally deferred per user instruction)
**Constitution version at design time**: 1.0.0

## Context

This repository is a personal fork of `casbin/redis-watcher` (via the `go-admin-team`
intermediate). The user is not the maintainer of the underlying library; the goal of this
spec-kit work is **not** to ship a feature but to capture a **precise behavioural baseline**
of what the library does today. Future modifications and upstream-compatibility checks will
be measured against the spec produced by this design.

The library is small (≈500 LOC across `watcher.go` and `options.go`, plus tests). The
graphify report (`graphify-out/GRAPH_REPORT.md`) shows 65 nodes / 7 communities — small
enough to spec in one document.

## Goal

Produce Spec Kit artifacts that lock down the existing public API contracts of redis-watcher
at "C-depth" (precise baseline), all-in-one, covering the entire library.

**Not in scope**: new features, refactoring, bug fixes. Acknowledged quirks are documented,
not corrected.

## Decisions

### D1. Output artifacts

Spec Kit standard files under a feature folder:

- `specs/001-retro-spec/spec.md` — user scenarios, functional requirements, success criteria,
  acknowledged quirks
- `specs/001-retro-spec/plan.md` — technical context (Go 1.20, redis/go-redis v9, casbin v2),
  as-built architecture, constitution-gate self-evaluation
- **No `tasks.md`** — there is no implementation work to schedule; the code already exists

This brainstorming design doc lives at `docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md`
(per superpowers default).

### D2. User stories

Four stories, mapped to existing tests in `watcher_test.go` for SC traceability:

| ID | Priority | Title | Existing test anchor |
|----|----------|-------|----------------------|
| US1 | P1 | Subscribe to peer policy updates | `TestUpdate*` family |
| US2 | P1 | Publish own policy updates | `TestUpdate*` (publish side) |
| US3 | P2 | IgnoreSelf to avoid echo | `TestWatcherWithIgnoreSelfTrue`, `TestWatcherWithIngnoreSelfFalse` (sic, kept as-is) |
| US4 | P2 | Cluster vs single-node parity | `TestWatcher` (single); cluster path covered structurally |

`NewPublishWatcher` is treated as a configuration variant of US2, not a separate story.

### D3. Functional requirements (the precise contracts)

The retro spec.md must lock down at minimum:

- **FR-Wire** — Wire format = `encoding/json` of `MSG{Method, ID, Sec, Ptype, OldRule,
  OldRules, NewRule, NewRules, FieldIndex, FieldValues}`. JSON-encoded by `MarshalBinary()`,
  decoded by `UnmarshalBinary()`. Per Constitution Principle V, adding fields is MINOR;
  reordering or removing fields is MAJOR.
- **FR-Methods** — Nine `UpdateType` constants: `Update`, `UpdateForSavePolicy`,
  `UpdateForAddPolicy`, `UpdateForRemovePolicy`, `UpdateForRemoveFilteredPolicy`,
  `UpdateForAddPolicies`, `UpdateForRemovePolicies`, `UpdateForUpdatePolicy`,
  `UpdateForUpdatePolicies`. Each has a corresponding `Watcher.Update*()` publishing method.
- **FR-IgnoreSelf** — Filter logic in `subscribe()`: `msg.ID == w.options.LocalID &&
  options.IgnoreSelf`. AND-of-two-conditions; either false → callback runs.
- **FR-Defaults** — `Channel = "/casbin"` and `LocalID = uuid.New().String()` only when the
  caller did not specify them (set in package-level `initConfig`).
- **FR-CallbackContract** — The registered callback receives the **raw JSON payload string**
  (`msg.Payload`), not a decoded `MSG`. The caller is responsible for `UnmarshalBinary` (or
  uses `DefaultUpdateCallback` which does it for them). This is the single most common
  misuse point and must be explicit in the spec.
- **FR-DefaultCallback** — `DefaultUpdateCallback(enforcer)` decodes and dispatches:
  `Update` and `UpdateForSavePolicy` → `enforcer.LoadPolicy()`; the other seven types call
  the corresponding `Self*` enforcer method (`SelfAddPolicy`, etc.). The `Self*` methods do
  not re-broadcast, which prevents a publish/subscribe loop.
- **FR-PublishOnly** — `NewPublishWatcher` runs only the package-level `initConfig` (which
  sets `Channel`/`LocalID` defaults) and **does not** call `w.initConfig` (which wires the
  callback and subscriber client). Result: publish-only watchers have no subscriber goroutine
  and no usable callback.
- **FR-ClientInjection** — `WatcherOptions.SubClient` and `PubClient` allow callers to inject
  pre-configured `*rds.Client` instances. The spec MUST call out the type asymmetry: option
  fields are concrete `*rds.Client`, but `Watcher.subClient` / `Watcher.pubClient` are typed
  as `rds.UniversalClient`. Consequence: callers cannot inject a cluster client through these
  fields — only single-node `*rds.Client`. Cluster injection requires the caller to use the
  `ClusterOptions` path instead.

### D4. Acknowledged quirks (documented, not fixed)

The retro spec.md will surface these in an explicit "Acknowledged Quirks" section with the
status against upstream `casbin/redis-watcher`:

- **Q1** — `Watcher.Close()` publishes the literal string `"Close"` on the channel; this is
  not valid `MSG` JSON, so peer subscribers log an unmarshal error. (Pattern is in
  `subscribe()`'s message-loop log line.)
- **Q2** — The `select { case <-w.close: return; default: }` check in `subscribe()` runs
  **after** the message is read but **before** unmarshalling, so it doesn't suppress the Q1
  log line on peers.
- **Q3** — README example imports `github.com/go-redis/redis/v8`, but the library actually
  uses `github.com/redis/go-redis/v9`. Already noted as technical debt in the constitution.
- **Q4** — Test function `TestWatcherWithIngnoreSelfFalse` carries an "Ingnore" typo;
  preserved historically. Not a correctness issue.

### D5. Success criteria

- **SC-1** — All 9 `UpdateType` constants documented with their wire-format MSG shape.
- **SC-2** — All 16 public functions/methods listed with stated contracts:
  - 3 constructors: `NewWatcher`, `NewWatcherWithCluster`, `NewPublishWatcher`
  - 1 free helper: `DefaultUpdateCallback`
  - 12 `Watcher` methods: `SetUpdateCallback`, `Update`, `UpdateForAddPolicy`,
    `UpdateForRemovePolicy`, `UpdateForRemoveFilteredPolicy`, `UpdateForSavePolicy`,
    `UpdateForAddPolicies`, `UpdateForRemovePolicies`, `UpdateForUpdatePolicy`,
    `UpdateForUpdatePolicies`, `GetWatcherOptions`, `Close`
  - Plus 2 `MSG` methods (`MarshalBinary`, `UnmarshalBinary`) and the exported types
    (`Watcher`, `WatcherOptions`, `MSG`, `UpdateType`) listed separately under "Types"
- **SC-3** — Each user story has at least one acceptance scenario that maps to an existing
  test in `watcher_test.go`.
- **SC-4** — Acknowledged Quirks section lists at least Q1–Q4.

### D6. Constitution gate self-evaluation (for the retro work itself)

| Principle | Status | Note |
|-----------|--------|------|
| I. Minimal Surface | N/A | No new exports |
| II. Test-First | N/A | Doc-only exemption (allowed by the constitution) |
| III. Upstream Compatibility | **applicable** | Spec must reconcile with upstream `casbin/redis-watcher` and document divergences |
| IV. Observability via Callbacks | N/A | No code change |
| V. SemVer | N/A | No public API change |
| Quality Gates | applicable | `gofmt -l .`, `go vet ./...`, `go test ./...` should remain green |

### D7. Branch strategy

Use the Spec Kit feature-branch flow when the user is ready to populate `specs/001-retro-spec/`:
running `/speckit-specify` triggers the existing `before_specify: speckit.git.feature` hook,
which creates the `001-retro-spec` branch. The retro spec lands on `main` via PR after review.

Fallback (if the user prefers): write directly on `main`. Faster, but skips the workflow's
review checkpoints.

### D8. Data sources

- `watcher.go`, `options.go` (already read in this session — full source captured)
- `watcher_test.go` (will read when drafting acceptance scenarios)
- `graphify-out/obsidian/*` (cross-checking community / hub mappings)
- `README.md` (the upstream-compat baseline; note the v8/v9 quirk)
- Upstream `casbin/redis-watcher` will **not** be auto-fetched. If a precise upstream-vs-fork
  text comparison is needed, the agent will surface it before reaching out.

## Out of scope (explicit)

- No code changes to `watcher.go` / `options.go` / tests.
- No upstream sync; no PR back to `casbin/redis-watcher`.
- No `tasks.md` artifact unless the user later asks for one.
- No transition to `writing-plans` from this brainstorm — the user explicitly deferred that
  step. The next time spec-kit work resumes here, populating `specs/001-retro-spec/spec.md`
  is the natural next move (likely via `/speckit-specify`).

## Approval

Approved by user (miso168net) on 2026-05-07 with the explicit instruction not to invoke the
`writing-plans` skill at the end of this brainstorm. The brainstorming checklist's
"transition to writing-plans" step is therefore skipped, not failed.
