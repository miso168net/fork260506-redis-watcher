---
type: community
cohesion: 0.21
members: 16
---

# Publish API & Wire Format

**Cohesion:** 0.21 - loosely connected
**Members:** 16 nodes

## Members
- [[.MarshalBinary()]] - code - watcher.go
- [[FR-Wire (JSON wire format of MSG)]] - rationale - docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md
- [[MSG]] - code - watcher.go
- [[MSG.MarshalBinary]] - code - watcher.go
- [[MSG.UnmarshalBinary]] - code - watcher.go
- [[US2 Publish own policy updates]] - rationale - docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md
- [[Watcher.Update]] - code - watcher.go
- [[Watcher.UpdateForAddPolicies]] - code - watcher.go
- [[Watcher.UpdateForAddPolicy]] - code - watcher.go
- [[Watcher.UpdateForRemoveFilteredPolicy]] - code - watcher.go
- [[Watcher.UpdateForRemovePolicies]] - code - watcher.go
- [[Watcher.UpdateForRemovePolicy]] - code - watcher.go
- [[Watcher.UpdateForSavePolicy]] - code - watcher.go
- [[Watcher.UpdateForUpdatePolicies]] - code - watcher.go
- [[Watcher.UpdateForUpdatePolicy]] - code - watcher.go
- [[Watcher.logRecord]] - code - watcher.go

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Publish_API__Wire_Format
SORT file.name ASC
```

## Connections to other communities
- 5 edges to [[_COMMUNITY_Watcher Tests & Lifecycle]]
- 4 edges to [[_COMMUNITY_Options & Initialization]]
- 2 edges to [[_COMMUNITY_Subscribe & Default Callback]]
- 1 edge to [[_COMMUNITY_Watcher API & Project Meta]]

## Top bridge nodes
- [[MSG]] - degree 18, connects to 3 communities
- [[MSG.UnmarshalBinary]] - degree 5, connects to 3 communities
- [[Watcher.Update]] - degree 7, connects to 1 community