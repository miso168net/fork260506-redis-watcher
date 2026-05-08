---
type: "query"
date: "2026-05-08T00:23:57.157313+00:00"
question: "Why does Watcher connect Watcher API & Project Meta to Watcher Tests & Lifecycle, Options & Initialization, Subscribe & Default Callback?"
contributor: "graphify"
source_nodes: ["Watcher", "initWatcherWithOptions", "WatcherOptions", "Watcher.subscribe", "DefaultUpdateCallback", "NewWatcher"]
---

# Q: Why does Watcher connect Watcher API & Project Meta to Watcher Tests & Lifecycle, Options & Initialization, Subscribe & Default Callback?

## Answer

Watcher is the only struct in this library that simultaneously owns state, the publish surface, the subscribe goroutine, lifecycle (Close), and options binding. Community 1 (Options) connects via WatcherOptions field embedding and the three constructors NewWatcher/NewWatcherWithCluster/NewPublishWatcher, all of which call Watcher.initConfig at watcher.go:182. Community 0 (Tests) connects via initWatcherWithOptions in watcher_test.go:16, which is the only test-side entrypoint and calls all constructors plus SetUpdateCallback; test teardown also calls .Close (watcher.go:480), pulling that method into the test community. Community 5 (Subscribe & Default Callback, cohesion 0.50) connects because Watcher.subscribe at watcher.go:429 is the goroutine that consumes Redis pub/sub messages, decodes via MSG.UnmarshalBinary at watcher.go:101, and dispatches to the registered callback, where DefaultUpdateCallback at watcher.go:28 needs a Watcher to bind to an enforcer. Community 2 (Watcher API & Project Meta) is Watcher's home, containing the Update* method family and meta nodes (Constitution v1.0.0, graphify rules, project tree snapshot) because retro spec and session-record docs all describe Watcher's behavior. Side note: AST-extracted methods (e.g. .subscribe()) and semantic-extracted methods (e.g. Watcher.subscribe) appear as separate nodes in different communities, inflating apparent cross-community fan-out without changing the conclusion. Watcher's centrality (betweenness 0.318) is the structural shadow of constitution Principle I (Library-First & Minimal Surface): one struct, one job, all roads pass through it.

## Source Nodes

- Watcher
- initWatcherWithOptions
- WatcherOptions
- Watcher.subscribe
- DefaultUpdateCallback
- NewWatcher