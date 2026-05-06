<!--
SYNC IMPACT REPORT
==================
Version change: (uninitialized template) → 1.0.0
Bump rationale: Initial ratification — first concrete content replacing all template placeholders. Establishes principles, constraints, and governance for the redis-watcher fork.

Modified principles:
  - [PRINCIPLE_1_NAME] → I. Library-First & Minimal Surface
  - [PRINCIPLE_2_NAME] → II. Test-First (NON-NEGOTIABLE)
  - [PRINCIPLE_3_NAME] → III. Upstream Compatibility
  - [PRINCIPLE_4_NAME] → IV. Observability via Callbacks
  - [PRINCIPLE_5_NAME] → V. Semantic Versioning Discipline

Added sections:
  - Technology & Compatibility Constraints (replaces [SECTION_2_*])
  - Development Workflow & Quality Gates (replaces [SECTION_3_*])
  - Governance (filled in)

Removed sections: none (all template placeholders consumed)

Templates requiring updates:
  - ✅ .specify/templates/plan-template.md — Constitution Check section populated with concrete gates
  - ✅ .specify/templates/spec-template.md — no change needed (no new mandatory spec sections introduced)
  - ⚠ pending .specify/templates/tasks-template.md — template marks tests as "OPTIONAL"; Principle II makes tests mandatory for any change to public behavior. Decide whether to project-override the template or rely on the Constitution Check gate to enforce.
  - ✅ .specify/templates/checklist-template.md — no constitution-driven changes required
  - ✅ README.md — no edits (README documents public API; constitution does not change it)
  - ✅ CLAUDE.md (project) — no edits (already references graphify workflow which Principle in Workflow section reinforces)

Follow-up TODOs: none deferred.
-->

# Redis Watcher (fork260506) Constitution

## Core Principles

### I. Library-First & Minimal Surface

This repository is a single-purpose Go library: a Casbin watcher implementation backed by Redis
pub/sub. It MUST remain a self-contained library with no CLI, no embedded service, and no
optional sub-packages added "just in case." The public API surface is intentionally small —
currently `NewWatcher`, `NewWatcherWithCluster`, `NewPublishWatcher`, `WatcherOptions`,
`DefaultUpdateCallback`, `UpdateType`, and the `Watcher` methods. New exported identifiers
require explicit justification in the change description; an existing function SHOULD be
extended via options before a new entry point is introduced.

**Rationale**: A thin adapter library survives best when its surface is predictable. Adding
exports is cheap to do and expensive to undo (semver-major), so the bias is toward saying no.

### II. Test-First (NON-NEGOTIABLE)

Any change to public behavior — message encoding, callback contracts, ignore-self semantics,
publish/subscribe wiring, options parsing — MUST be covered by a failing test in
`watcher_test.go` (or a sibling `*_test.go`) before the implementation lands. The
Red → Green → Refactor cycle is mandatory. Pure refactors that do not change behavior MAY
skip the red step but MUST still pass `go test ./...` before and after.

Exemptions (must be stated explicitly in the change description, not assumed):
documentation-only edits, comment fixes, dependency bumps that pass the existing suite
unchanged, and tooling/config files outside the Go build.

**Rationale**: This package is a coordination primitive — silent regressions cause policy
drift in every downstream service. Tests are the only durable contract.

### III. Upstream Compatibility

This repo is a personal fork of `casbin/redis-watcher` (via `go-admin-team/redis-watcher`).
Public API parity with upstream `casbin/redis-watcher` SHOULD be preserved by default. Any
intentional divergence MUST:

1. Be recorded in a fork-provenance document under the repo root (e.g. `x_fork.*.md`), not
   only in commit messages.
2. Keep the upstream-compatible call shape callable, or document the migration path.

Pulling new commits from upstream MUST NOT silently drop fork-specific changes; conflicts
require an explicit decision recorded in the same provenance document.

**Rationale**: A fork that drifts arbitrarily loses the ability to pull upstream fixes. The
provenance document (`x_fork.branch-origin.md` already exists) is the single source of truth
for "why does our copy differ."

### IV. Observability via Callbacks

The watcher's reason to exist is to surface policy-change events. Every code path that
receives a Redis message MUST flow through a registered callback (`SetUpdateCallback` or
`SetUpdateCallbackEx`) before being considered "delivered." Silent drops, swallowed errors,
or fallback paths that bypass the callback are forbidden. Errors that occur during decode or
dispatch MUST be returned to the caller or surfaced through the watcher's error channel —
never logged-and-ignored.

**Rationale**: A watcher that loses an event without telling anyone is worse than no watcher
at all, because it produces a false sense of synchronization.

### V. Semantic Versioning Discipline

The module path is versioned (`/v2`). Releases MUST follow SemVer:

- **MAJOR**: any change to an exported identifier's signature, removal of an export, change
  to message-wire format, or change to default behavior of `WatcherOptions`. Requires a new
  module path suffix (`/v3`, ...).
- **MINOR**: new exported identifier, new option field with a backward-compatible default,
  new optional callback hook.
- **PATCH**: bug fixes, dependency bumps that don't change observable behavior,
  documentation, internal refactors.

The `Sync Impact Report` block in the constitution and the changelog (when introduced) MUST
agree on the bump category for any release.

**Rationale**: Downstream Casbin users pin by module path; an accidental breaking change in a
"minor" release breaks their builds and erodes trust in the fork.

## Technology & Compatibility Constraints

- **Language floor**: Go 1.20 (as declared in `go.mod`). Raising the floor is a MINOR change
  and requires updating CI and the README installation note.
- **Redis client**: `github.com/redis/go-redis/v9`. The README example still shows the older
  `go-redis/redis/v8` import — that discrepancy is acknowledged technical debt; new code
  MUST use the v9 client and any README update should reflect v9.
- **License**: Apache 2.0 (inherited from upstream). Re-licensing is forbidden.
- **Dependencies**: New direct dependencies require justification in the change description.
  Prefer the standard library; prefer existing transitive dependencies (`google/uuid`,
  `casbin/casbin/v2`, `redis/go-redis/v9`) over introducing parallel ones.
- **Wire format**: The `MSG` struct's binary marshalling is part of the public contract.
  Adding fields is a MINOR change only if old consumers can still decode the message;
  reordering or removing fields is a MAJOR change.

## Development Workflow & Quality Gates

- **Pre-merge gates**: `go test ./...` MUST pass; `go vet ./...` MUST be clean; `gofmt -l .`
  MUST produce no output.
- **Test scope**: Changes touching `watcher.go` or `options.go` MUST run the full
  `watcher_test.go` suite (it covers add/remove/update policy flows and ignore-self
  semantics). Changes only to docs/examples MAY skip the suite if explicitly noted.
- **Graphify hygiene**: After any structural change to Go source files, run
  `graphify update .` to refresh `graphify-out/` per the project `CLAUDE.md`. The graph is
  the navigation aid for future agent sessions; letting it rot makes onboarding slower.
- **Public API changes**: A PR/commit that changes the public API MUST update the README
  example AND the fork-provenance document if the change diverges from upstream.
- **Commit boundaries**: Each commit SHOULD represent one logical change. Mixing a
  dependency bump with a behavior change in one commit is discouraged because it makes
  bisecting future regressions painful.

## Governance

This constitution supersedes ad-hoc preferences when the two conflict. It does NOT supersede
explicit instructions from the repository owner in the active conversation — those always
win (per the Instruction Priority rules in `superpowers:using-superpowers`).

**Amendment procedure**:

1. Open or update a constitution proposal (this file) describing the change and its
   rationale.
2. Bump `Version` per the Semantic Versioning Discipline principle (MAJOR/MINOR/PATCH rules
   apply to the constitution itself).
3. Update `Last Amended` to the date of the change (ISO `YYYY-MM-DD`).
4. Run the consistency-propagation checklist from `/speckit-constitution` to update
   dependent templates and surface unresolved follow-ups in the Sync Impact Report.

**Compliance review**: The `Constitution Check` gate in `.specify/templates/plan-template.md`
is the enforcement point — every `/speckit-plan` run MUST evaluate the principles above and
record any deliberate violation in the plan's `Complexity Tracking` table with a stated
justification. A violation without a justification is a blocker, not a suggestion.

**Runtime guidance**: The project `CLAUDE.md` and global `~/.claude/CLAUDE.md` are the
day-to-day operational guides. The constitution is the slow-changing layer beneath them; if
the two ever conflict on a non-negotiable rule, raise it as an amendment rather than
silently following the operational guide.

**Version**: 1.0.0 | **Ratified**: 2026-05-07 | **Last Amended**: 2026-05-07
