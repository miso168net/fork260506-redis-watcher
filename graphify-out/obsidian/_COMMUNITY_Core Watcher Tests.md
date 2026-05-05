---
type: community
cohesion: 0.48
members: 7
---

# Core Watcher Tests

**Cohesion:** 0.48 - moderately connected
**Members:** 7 nodes

## Members
- [[.SetUpdateCallback()]] - code - watcher.go
- [[.Update()]] - code - watcher.go
- [[TestUpdate()]] - code - watcher_test.go
- [[TestWatcher()]] - code - watcher_test.go
- [[TestWatcherWithIgnoreSelfTrue()]] - code - watcher_test.go
- [[TestWatcherWithIngnoreSelfFalse()]] - code - watcher_test.go
- [[initWatcher()]] - code - watcher_test.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Core_Watcher_Tests
SORT file.name ASC
```

## Connections to other communities
- 13 edges to [[_COMMUNITY_Update Policy Tests]]
- 3 edges to [[_COMMUNITY_Watcher Update API]]
- 2 edges to [[_COMMUNITY_Watcher Impl & Message Codec]]

## Top bridge nodes
- [[.SetUpdateCallback()]] - degree 7, connects to 3 communities
- [[TestUpdate()]] - degree 6, connects to 2 communities
- [[.Update()]] - degree 6, connects to 1 community
- [[TestWatcher()]] - degree 5, connects to 1 community
- [[TestWatcherWithIgnoreSelfTrue()]] - degree 5, connects to 1 community