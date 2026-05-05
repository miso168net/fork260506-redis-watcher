---
type: community
cohesion: 0.27
members: 11
---

# Watcher Impl & Message Codec

**Cohesion:** 0.27 - loosely connected
**Members:** 11 nodes

## Members
- [[.MarshalBinary()]] - code - watcher.go
- [[.UnmarshalBinary()]] - code - watcher.go
- [[.initConfig()]] - code - watcher.go
- [[.subscribe()]] - code - watcher.go
- [[DefaultUpdateCallback()]] - code - watcher.go
- [[MSG]] - code - watcher.go
- [[NewPublishWatcher()]] - code - watcher.go
- [[NewWatcher()]] - code - watcher.go
- [[NewWatcherWithCluster()]] - code - watcher.go
- [[UpdateType]] - code - watcher.go
- [[watcher.go]] - code - watcher.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Watcher_Impl_&_Message_Codec
SORT file.name ASC
```

## Connections to other communities
- 4 edges to [[_COMMUNITY_Update Policy Tests]]
- 3 edges to [[_COMMUNITY_Watcher Update API]]
- 2 edges to [[_COMMUNITY_Core Watcher Tests]]

## Top bridge nodes
- [[.initConfig()]] - degree 5, connects to 2 communities
- [[.subscribe()]] - degree 5, connects to 2 communities
- [[watcher.go]] - degree 7, connects to 1 community
- [[.UnmarshalBinary()]] - degree 4, connects to 1 community
- [[NewWatcher()]] - degree 4, connects to 1 community