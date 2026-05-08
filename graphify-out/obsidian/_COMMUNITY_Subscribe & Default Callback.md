---
type: community
cohesion: 0.50
members: 4
---

# Subscribe & Default Callback

**Cohesion:** 0.50 - moderately connected
**Members:** 4 nodes

## Members
- [[.UnmarshalBinary()]] - code - watcher.go
- [[.subscribe()]] - code - watcher.go
- [[DefaultUpdateCallback()]] - code - watcher.go
- [[FR-DefaultCallback (dispatch via Self)]] - rationale - docs/superpowers/specs/2026-05-07-redis-watcher-retro-spec-design.md

## Live Query (requires Dataview plugin)

```dataview
TABLE source_file, type FROM #community/Subscribe__Default_Callback
SORT file.name ASC
```

## Connections to other communities
- 3 edges to [[_COMMUNITY_Options & Initialization]]
- 3 edges to [[_COMMUNITY_Watcher Tests & Lifecycle]]
- 2 edges to [[_COMMUNITY_Publish API & Wire Format]]
- 1 edge to [[_COMMUNITY_Watcher API & Project Meta]]
- 1 edge to [[_COMMUNITY_Fork Provenance & README]]

## Top bridge nodes
- [[DefaultUpdateCallback()]] - degree 6, connects to 4 communities
- [[.subscribe()]] - degree 5, connects to 3 communities
- [[.UnmarshalBinary()]] - degree 4, connects to 2 communities