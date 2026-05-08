---
type: community
cohesion: 0.14
members: 21
---

# Options & Initialization

**Cohesion:** 0.14 - loosely connected
**Members:** 21 nodes

## Members
- [[.initConfig()]] - code - watcher.go
- [[FR-CallbackContract (raw JSON payload)]] - rationale - docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md
- [[FR-ClientInjection (type asymmetry)]] - rationale - docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md
- [[FR-Defaults (Channel and LocalID defaults)]] - rationale - docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md
- [[FR-IgnoreSelf (filter logic)]] - rationale - docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md
- [[FR-Methods (nine UpdateType constants)]] - rationale - docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md
- [[FR-PublishOnly (NewPublishWatcher gap)]] - rationale - docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md
- [[NewPublishWatcher()]] - code - watcher.go
- [[NewWatcher()]] - code - watcher.go
- [[NewWatcherWithCluster()]] - code - watcher.go
- [[Q2 select close-check ordering quirk]] - rationale - docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md
- [[Struct-options pattern (functional options degenerate)]] - rationale - x_fork.tree-20260506.md
- [[US4 Cluster vs single-node parity]] - rationale - docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md
- [[UpdateType]] - code - watcher.go
- [[Watcher.SetUpdateCallback]] - code - watcher.go
- [[Watcher.initConfig]] - code - watcher.go
- [[Watcher.subscribe]] - code - watcher.go
- [[WatcherOptions]] - code - options.go
- [[initConfig()]] - code - options.go
- [[options.go]] - code - options.go
- [[watcher.go]] - code - watcher.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Options__Initialization
SORT file.name ASC
```

## Connections to other communities
- 6 edges to [[_COMMUNITY_Watcher API & Project Meta]]
- 4 edges to [[_COMMUNITY_Publish API & Wire Format]]
- 4 edges to [[_COMMUNITY_Watcher Tests & Lifecycle]]
- 3 edges to [[_COMMUNITY_Subscribe & Default Callback]]
- 2 edges to [[_COMMUNITY_Fork Provenance & README]]

## Top bridge nodes
- [[NewWatcherWithCluster()]] - degree 9, connects to 3 communities
- [[NewWatcher()]] - degree 8, connects to 3 communities
- [[watcher.go]] - degree 7, connects to 3 communities
- [[.initConfig()]] - degree 5, connects to 2 communities
- [[UpdateType]] - degree 4, connects to 2 communities