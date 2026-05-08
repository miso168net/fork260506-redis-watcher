---
source_file: "watcher_test.go"
type: "code"
community: "Watcher Tests & Lifecycle"
location: "L91"
tags:
  - graphify/code
  - graphify/EXTRACTED
  - community/Watcher_Tests__Lifecycle
---

# TestUpdate()

## Connections
- [[.Close()]] - `calls` [INFERRED]
- [[.SetUpdateCallback()]] - `calls` [INFERRED]
- [[.UnmarshalBinary()]] - `calls` [INFERRED]
- [[.Update()]] - `calls` [INFERRED]
- [[MSG.UnmarshalBinary]] - `calls` [EXTRACTED]
- [[US1 Subscribe to peer policy updates]] - `references` [EXTRACTED]
- [[Watcher.Update]] - `calls` [EXTRACTED]
- [[initWatcher()]] - `calls` [EXTRACTED]
- [[watcher_test.go]] - `contains` [EXTRACTED]

#graphify/code #graphify/EXTRACTED #community/Watcher_Tests__Lifecycle