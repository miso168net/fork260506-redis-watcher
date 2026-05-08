---
source_file: "watcher_test.go"
type: "code"
community: "Watcher Tests & Lifecycle"
location: "L75"
tags:
  - graphify/code
  - graphify/EXTRACTED
  - community/Watcher_Tests__Lifecycle
---

# TestWatcherWithIgnoreSelfTrue()

## Connections
- [[.Close()]] - `calls` [INFERRED]
- [[.SetUpdateCallback()]] - `calls` [INFERRED]
- [[.Update()]] - `calls` [INFERRED]
- [[US3 IgnoreSelf to avoid echo]] - `references` [EXTRACTED]
- [[Watcher.Update]] - `calls` [EXTRACTED]
- [[initWatcherWithOptions()]] - `calls` [EXTRACTED]
- [[watcher_test.go]] - `contains` [EXTRACTED]

#graphify/code #graphify/EXTRACTED #community/Watcher_Tests__Lifecycle