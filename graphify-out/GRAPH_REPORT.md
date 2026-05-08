# Graph Report - .  (2026-05-08)

## Corpus Check
- Corpus is ~4,906 words - fits in a single context window. You may not need a graph.

## Summary
- 96 nodes · 190 edges · 6 communities (5 shown, 1 thin omitted)
- Extraction: 87% EXTRACTED · 13% INFERRED · 0% AMBIGUOUS · INFERRED: 25 edges (avg confidence: 0.8)
- Token cost: 51,638 input · 12,909 output

## Community Hubs (Navigation)
- [[_COMMUNITY_Watcher Tests & Lifecycle|Watcher Tests & Lifecycle]]
- [[_COMMUNITY_Options & Initialization|Options & Initialization]]
- [[_COMMUNITY_Watcher API & Project Meta|Watcher API & Project Meta]]
- [[_COMMUNITY_Publish API & Wire Format|Publish API & Wire Format]]
- [[_COMMUNITY_Fork Provenance & README|Fork Provenance & README]]
- [[_COMMUNITY_Subscribe & Default Callback|Subscribe & Default Callback]]

## God Nodes (most connected - your core abstractions)
1. `Watcher` - 22 edges
2. `initWatcherWithOptions()` - 19 edges
3. `MSG` - 18 edges
4. `WatcherOptions` - 9 edges
5. `NewWatcherWithCluster()` - 9 edges
6. `TestUpdate()` - 9 edges
7. `Watcher.logRecord` - 9 edges
8. `Redis Watcher (project)` - 9 edges
9. `NewWatcher()` - 8 edges
10. `TestWatcherWithIngnoreSelfFalse()` - 8 edges

## Surprising Connections (you probably didn't know these)
- `Redis Watcher (project)` --semantically_similar_to--> `casbin/redis-watcher (upstream)`  [INFERRED] [semantically similar]
  README.md → x_fork.branch-origin.md
- `WatcherOptions` --references--> `Project tree snapshot 2026-05-06`  [EXTRACTED]
  options.go → x_fork.tree-20260506.md
- `WatcherOptions` --rationale_for--> `Struct-options pattern (functional options degenerate)`  [EXTRACTED]
  options.go → x_fork.tree-20260506.md
- `WatcherOptions` --references--> `Redis Watcher Retro Spec Design`  [EXTRACTED]
  options.go → docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md
- `WatcherOptions` --rationale_for--> `FR-ClientInjection (type asymmetry)`  [EXTRACTED]
  options.go → docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md

## Hyperedges (group relationships)
- **Policy publish/subscribe flow** — watcher_subscribe, watcher_msg, watcher_defaultupdatecallback, watcher_setupdatecallback, watcher_updatetype [EXTRACTED 0.90]
- **Watcher construction paths (single, cluster, publish-only)** — watcher_newwatcher, watcher_newwatcherwithcluster, watcher_newpublishwatcher, watcher_initconfig, options_initconfig [EXTRACTED 0.90]
- **Retro spec baseline capture (design + sources)** — retrospec_design_doc, watcher_watcher, options_watcheroptions, watcher_msg, graphify_session_20260506 [INFERRED 0.85]

## Communities (6 total, 1 thin omitted)

### Community 0 - "Watcher Tests & Lifecycle"
Cohesion: 0.2
Nodes (20): Cross-module call extraction limit, Q1: Close publishes literal Close string, Q4: Ingnore typo in test name, US1: Subscribe to peer policy updates, US3: IgnoreSelf to avoid echo, Watcher.Close, initWatcher(), initWatcherWithOptions() (+12 more)

### Community 1 - "Options & Initialization"
Cohesion: 0.14
Nodes (18): initConfig(), WatcherOptions, FR-CallbackContract (raw JSON payload), FR-ClientInjection (type asymmetry), FR-Defaults (Channel and LocalID defaults), FR-IgnoreSelf (filter logic), FR-Methods (nine UpdateType constants), FR-PublishOnly (NewPublishWatcher gap) (+10 more)

### Community 2 - "Watcher API & Project Meta"
Cohesion: 0.16
Nodes (8): Project graphify rules (CLAUDE.md), God-node topology finding (Watcher), graphify session 2026-05-06, Constitution v1.0.0, Redis Watcher Retro Spec Design, Single-package layout convention, Project tree snapshot 2026-05-06, Watcher

### Community 3 - "Publish API & Wire Format"
Cohesion: 0.21
Nodes (15): FR-Wire (JSON wire format of MSG), US2: Publish own policy updates, Watcher.logRecord, MSG.MarshalBinary, MSG, MSG.UnmarshalBinary, Watcher.Update, Watcher.UpdateForAddPolicies (+7 more)

### Community 4 - "Fork Provenance & README"
Cohesion: 0.17
Nodes (12): miso168net/fork260506-redis-watcher, HEAD bfe327c (Go 1.20 upgrade), go-admin-team/redis-watcher (intermediate), main branch origin record, Rationale: unify default branch as main, casbin/redis-watcher (upstream), Apache 2.0 License, Casbin (+4 more)

## Knowledge Gaps
- **27 isolated node(s):** `Project graphify rules (CLAUDE.md)`, `Casbin`, `go-redis`, `Apache 2.0 License`, `go-admin-team/redis-watcher (intermediate)` (+22 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **1 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Watcher` connect `Watcher API & Project Meta` to `Watcher Tests & Lifecycle`, `Options & Initialization`, `Subscribe & Default Callback`?**
  _High betweenness centrality (0.318) - this node is a cross-community bridge._
- **Why does `MSG` connect `Publish API & Wire Format` to `Options & Initialization`, `Watcher API & Project Meta`, `Subscribe & Default Callback`?**
  _High betweenness centrality (0.231) - this node is a cross-community bridge._
- **Why does `initWatcherWithOptions()` connect `Watcher Tests & Lifecycle` to `Options & Initialization`, `Watcher API & Project Meta`, `Subscribe & Default Callback`?**
  _High betweenness centrality (0.171) - this node is a cross-community bridge._
- **What connects `Project graphify rules (CLAUDE.md)`, `Casbin`, `go-redis` to the rest of the system?**
  _27 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `Options & Initialization` be split into smaller, more focused modules?**
  _Cohesion score 0.14 - nodes in this community are weakly interconnected._