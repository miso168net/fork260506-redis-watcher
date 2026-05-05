---
type: community
cohesion: 0.45
members: 11
---

# Update Policy Tests

**Cohesion:** 0.45 - moderately connected
**Members:** 11 nodes

## Members
- [[.Close()]] - code - watcher.go
- [[TestUpdateForAddPolicies()]] - code - watcher_test.go
- [[TestUpdateForAddPolicy()]] - code - watcher_test.go
- [[TestUpdateForRemoveFilteredPolicy()]] - code - watcher_test.go
- [[TestUpdateForRemovePolicies()]] - code - watcher_test.go
- [[TestUpdateForRemovePolicy()]] - code - watcher_test.go
- [[TestUpdateForUpdatePolicies()]] - code - watcher_test.go
- [[TestUpdateForUpdatePolicy()]] - code - watcher_test.go
- [[TestUpdateSavePolicy()]] - code - watcher_test.go
- [[initWatcherWithOptions()]] - code - watcher_test.go
- [[watcher_test.go]] - code - watcher_test.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Update_Policy_Tests
SORT file.name ASC
```

## Connections to other communities
- 13 edges to [[_COMMUNITY_Core Watcher Tests]]
- 4 edges to [[_COMMUNITY_Watcher Impl & Message Codec]]
- 1 edge to [[_COMMUNITY_Watcher Update API]]

## Top bridge nodes
- [[.Close()]] - degree 14, connects to 3 communities
- [[initWatcherWithOptions()]] - degree 16, connects to 2 communities
- [[watcher_test.go]] - degree 14, connects to 1 community