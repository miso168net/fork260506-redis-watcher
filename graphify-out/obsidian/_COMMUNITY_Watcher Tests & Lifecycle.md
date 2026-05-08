---
type: community
cohesion: 0.20
members: 24
---

# Watcher Tests & Lifecycle

**Cohesion:** 0.20 - loosely connected
**Members:** 24 nodes

## Members
- [[.Close()]] - code - watcher.go
- [[.SetUpdateCallback()]] - code - watcher.go
- [[.Update()]] - code - watcher.go
- [[Cross-module call extraction limit]] - rationale - x_fork.graphify-20260506.md
- [[Q1 Close publishes literal Close string]] - rationale - docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md
- [[Q4 Ingnore typo in test name]] - rationale - docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md
- [[TestUpdate()]] - code - watcher_test.go
- [[TestUpdateForAddPolicies()]] - code - watcher_test.go
- [[TestUpdateForAddPolicy()]] - code - watcher_test.go
- [[TestUpdateForRemoveFilteredPolicy()]] - code - watcher_test.go
- [[TestUpdateForRemovePolicies()]] - code - watcher_test.go
- [[TestUpdateForRemovePolicy()]] - code - watcher_test.go
- [[TestUpdateForUpdatePolicies()]] - code - watcher_test.go
- [[TestUpdateForUpdatePolicy()]] - code - watcher_test.go
- [[TestUpdateSavePolicy()]] - code - watcher_test.go
- [[TestWatcher()]] - code - watcher_test.go
- [[TestWatcherWithIgnoreSelfTrue()]] - code - watcher_test.go
- [[TestWatcherWithIngnoreSelfFalse()]] - code - watcher_test.go
- [[US1 Subscribe to peer policy updates]] - rationale - docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md
- [[US3 IgnoreSelf to avoid echo]] - rationale - docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md
- [[Watcher.Close]] - code - watcher.go
- [[initWatcher()]] - code - watcher_test.go
- [[initWatcherWithOptions()]] - code - watcher_test.go
- [[watcher_test.go]] - code - watcher_test.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Watcher_Tests__Lifecycle
SORT file.name ASC
```

## Connections to other communities
- 5 edges to [[_COMMUNITY_Watcher API & Project Meta]]
- 5 edges to [[_COMMUNITY_Publish API & Wire Format]]
- 4 edges to [[_COMMUNITY_Options & Initialization]]
- 3 edges to [[_COMMUNITY_Subscribe & Default Callback]]

## Top bridge nodes
- [[initWatcherWithOptions()]] - degree 19, connects to 3 communities
- [[.Close()]] - degree 14, connects to 2 communities
- [[TestUpdate()]] - degree 9, connects to 2 communities
- [[.SetUpdateCallback()]] - degree 7, connects to 2 communities
- [[TestWatcherWithIngnoreSelfFalse()]] - degree 8, connects to 1 community