---
type: community
cohesion: 0.16
members: 19
---

# Watcher API & Project Meta

**Cohesion:** 0.16 - loosely connected
**Members:** 19 nodes

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
- [[Constitution v1.0.0]] - document - docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md
- [[God-node topology finding (Watcher)]] - rationale - x_fork.graphify-20260506.md
- [[Project graphify rules (CLAUDE.md)]] - document - CLAUDE.md
- [[Project tree snapshot 2026-05-06]] - document - x_fork.tree-20260506.md
- [[Redis Watcher Retro Spec Design]] - document - docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md
- [[Single-package layout convention]] - rationale - x_fork.tree-20260506.md
- [[Watcher]] - code - watcher.go
- [[graphify session 2026-05-06]] - document - x_fork.graphify-20260506.md

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Watcher_API__Project_Meta
SORT file.name ASC
```

## Connections to other communities
- 6 edges to [[_COMMUNITY_Options & Initialization]]
- 5 edges to [[_COMMUNITY_Watcher Tests & Lifecycle]]
- 1 edge to [[_COMMUNITY_Subscribe & Default Callback]]
- 1 edge to [[_COMMUNITY_Publish API & Wire Format]]
- 1 edge to [[_COMMUNITY_Fork Provenance & README]]

## Top bridge nodes
- [[Watcher]] - degree 22, connects to 3 communities
- [[Redis Watcher Retro Spec Design]] - degree 6, connects to 2 communities
- [[Project tree snapshot 2026-05-06]] - degree 5, connects to 2 communities
- [[.logRecord()]] - degree 10, connects to 1 community
- [[graphify session 2026-05-06]] - degree 5, connects to 1 community