# Graph Report - .  (2026-05-06)

## Corpus Check
- Corpus is ~2,485 words - fits in a single context window. You may not need a graph.

## Summary
- 65 nodes · 122 edges · 7 communities detected
- Extraction: 77% EXTRACTED · 21% INFERRED · 2% AMBIGUOUS · INFERRED: 26 edges (avg confidence: 0.8)
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- [[_COMMUNITY_Watcher Update API|Watcher Update API]]
- [[_COMMUNITY_README & Public Surface|README & Public Surface]]
- [[_COMMUNITY_Watcher Impl & Message Codec|Watcher Impl & Message Codec]]
- [[_COMMUNITY_Update Policy Tests|Update Policy Tests]]
- [[_COMMUNITY_Fork Branch Provenance|Fork Branch Provenance]]
- [[_COMMUNITY_Core Watcher Tests|Core Watcher Tests]]
- [[_COMMUNITY_Watcher Options Config|Watcher Options Config]]

## God Nodes (most connected - your core abstractions)
1. `Watcher` - 17 edges
2. `initWatcherWithOptions()` - 16 edges
3. `Redis Watcher` - 9 edges
4. `TestUpdate()` - 6 edges
5. `TestWatcher()` - 5 edges
6. `TestWatcherWithIngnoreSelfFalse()` - 5 edges
7. `TestWatcherWithIgnoreSelfTrue()` - 5 edges
8. `miso168net/fork260506-redis-watcher` - 5 edges
9. `NewWatcher()` - 4 edges
10. `NewWatcherWithCluster()` - 4 edges

## Surprising Connections (you probably didn't know these)
- `casbin/redis-watcher (upstream)` --semantically_similar_to--> `Redis Watcher`  [INFERRED] [semantically similar]
  x_fork.branch-origin.md → README.md
- `initWatcherWithOptions()` --calls--> `DefaultUpdateCallback()`  [INFERRED]
  watcher_test.go → watcher.go
- `initWatcherWithOptions()` --calls--> `NewWatcher()`  [INFERRED]
  watcher_test.go → watcher.go
- `initWatcherWithOptions()` --calls--> `NewWatcherWithCluster()`  [INFERRED]
  watcher_test.go → watcher.go

## Hyperedges (group relationships)
- **Watcher setup flow (init -> bind enforcer -> set callback)** — readme_new_watcher, readme_set_watcher, readme_set_update_callback, readme_enforcer [EXTRACTED 1.00]

## Communities

### Community 0 - "Watcher Update API"
Cohesion: 0.29
Nodes (1): Watcher

### Community 1 - "README & Public Surface"
Cohesion: 0.21
Nodes (12): Apache 2.0 License, Casbin, DefaultUpdateCallback, Casbin Enforcer, go-redis, NewWatcher, NewWatcherWithCluster, Redis (+4 more)

### Community 2 - "Watcher Impl & Message Codec"
Cohesion: 0.27
Nodes (6): DefaultUpdateCallback(), MSG, NewPublishWatcher(), NewWatcher(), NewWatcherWithCluster(), UpdateType

### Community 3 - "Update Policy Tests"
Cohesion: 0.45
Nodes (9): initWatcherWithOptions(), TestUpdateForAddPolicies(), TestUpdateForAddPolicy(), TestUpdateForRemoveFilteredPolicy(), TestUpdateForRemovePolicies(), TestUpdateForRemovePolicy(), TestUpdateForUpdatePolicies(), TestUpdateForUpdatePolicy() (+1 more)

### Community 4 - "Fork Branch Provenance"
Cohesion: 0.28
Nodes (9): main branch origin record, HEAD bfe327c (Go 1.20 upgrade), go-admin-team/redis-watcher (intermediate), main branch, master branch, Rationale: unify default branch as main, Rationale: no squash/rebase, history preserved, miso168net/fork260506-redis-watcher (+1 more)

### Community 5 - "Core Watcher Tests"
Cohesion: 0.48
Nodes (5): initWatcher(), TestUpdate(), TestWatcher(), TestWatcherWithIgnoreSelfTrue(), TestWatcherWithIngnoreSelfFalse()

### Community 6 - "Watcher Options Config"
Cohesion: 0.67
Nodes (1): WatcherOptions

## Ambiguous Edges - Review These
- `miso168net/fork260506-redis-watcher` → `go-admin-team/redis-watcher (intermediate)`  [AMBIGUOUS]
  x_fork.branch-origin.md · relation: references
- `casbin/redis-watcher (upstream)` → `go-admin-team/redis-watcher (intermediate)`  [AMBIGUOUS]
  x_fork.branch-origin.md · relation: references

## Knowledge Gaps
- **8 isolated node(s):** `WatcherOptions`, `UpdateType`, `Redis`, `go-redis`, `Apache 2.0 License` (+3 more)
  These have ≤1 connection - possible missing edges or undocumented components.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **What is the exact relationship between `miso168net/fork260506-redis-watcher` and `go-admin-team/redis-watcher (intermediate)`?**
  _Edge tagged AMBIGUOUS (relation: references) - confidence is low._
- **What is the exact relationship between `casbin/redis-watcher (upstream)` and `go-admin-team/redis-watcher (intermediate)`?**
  _Edge tagged AMBIGUOUS (relation: references) - confidence is low._
- **Why does `Watcher` connect `Watcher Update API` to `Watcher Impl & Message Codec`, `Update Policy Tests`, `Core Watcher Tests`?**
  _High betweenness centrality (0.181) - this node is a cross-community bridge._
- **Why does `Redis Watcher` connect `README & Public Surface` to `Fork Branch Provenance`?**
  _High betweenness centrality (0.071) - this node is a cross-community bridge._
- **Why does `initWatcherWithOptions()` connect `Update Policy Tests` to `Watcher Impl & Message Codec`, `Core Watcher Tests`?**
  _High betweenness centrality (0.060) - this node is a cross-community bridge._
- **Are the 4 inferred relationships involving `initWatcherWithOptions()` (e.g. with `NewWatcherWithCluster()` and `NewWatcher()`) actually correct?**
  _`initWatcherWithOptions()` has 4 INFERRED edges - model-reasoned connections that need verification._
- **Are the 4 inferred relationships involving `TestUpdate()` (e.g. with `.SetUpdateCallback()` and `.UnmarshalBinary()`) actually correct?**
  _`TestUpdate()` has 4 INFERRED edges - model-reasoned connections that need verification._