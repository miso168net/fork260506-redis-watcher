---
type: community
cohesion: 0.29
members: 12
---

# Watcher Update API

**Cohesion:** 0.29 - loosely connected
**Members:** 12 nodes

## Members
- [[.GetWatcherOptions()]] - code - watcher.go
- [[.UpdateForAddPolicies()]] - code - watcher.go
- [[.UpdateForAddPolicy()]] - code - watcher.go
- [[.UpdateForRemoveFilteredPolicy()]] - code - watcher.go
- [[.UpdateForRemovePolicies()]] - code - watcher.go
- [[.UpdateForRemovePolicy()]] - code - watcher.go
- [[.UpdateForSavePolicy()]] - code - watcher.go
- [[.UpdateForUpdatePolicies()]] - code - watcher.go
- [[.UpdateForUpdatePolicy()]] - code - watcher.go
- [[.logRecord()]] - code - watcher.go
- [[.unsubscribe()]] - code - watcher.go
- [[Watcher]] - code - watcher.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Watcher_Update_API
SORT file.name ASC
```

## Connections to other communities
- 3 edges to [[_COMMUNITY_Watcher Impl & Message Codec]]
- 3 edges to [[_COMMUNITY_Core Watcher Tests]]
- 1 edge to [[_COMMUNITY_Update Policy Tests]]

## Top bridge nodes
- [[Watcher]] - degree 17, connects to 3 communities
- [[.logRecord()]] - degree 10, connects to 1 community