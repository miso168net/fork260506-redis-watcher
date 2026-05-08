---
type: "query"
date: "2026-05-08T00:28:00.338065+00:00"
question: "Why does MSG connect Publish API & Wire Format to Options & Initialization, Watcher API & Project Meta, Subscribe & Default Callback?"
contributor: "graphify"
source_nodes: ["MSG", "UpdateType", "MSG.MarshalBinary", "MSG.UnmarshalBinary", "Watcher.subscribe", "DefaultUpdateCallback", "FR-Wire"]
---

# Q: Why does MSG connect Publish API & Wire Format to Options & Initialization, Watcher API & Project Meta, Subscribe & Default Callback?

## Answer

MSG is a pivot-data bridge (vs Watcher's owner-of-state bridge). Its betweenness 0.231 reflects that every publish and every subscribe must touch this single data structure. (1) Community 3 (its home, Publish API & Wire Format) groups MSG with its codec methods MarshalBinary/UnmarshalBinary at watcher.go:96-101 and with the nine semantic-extracted Watcher.UpdateFor* methods that each populate an MSG and call PUBLISH. FR-Wire is the spec-side rationale_for the codec methods. (2) Community 5 (Subscribe & Default Callback) bridges via Watcher.subscribe at watcher.go:429 calling MSG.UnmarshalBinary on incoming bytes; DefaultUpdateCallback at watcher.go:28 also begins with UnmarshalBinary before dispatch. So MSG is the unique data form on the consumption side too. (3) Community 1 (Options & Initialization) bridges via UpdateType at watcher.go:82, since MSG.Method's type is UpdateType. UpdateType lives in C1 because community detection groups it with WatcherOptions as configuration enums. FR-Methods, FR-IgnoreSelf, and the Q2 close-check quirk all sit in C1 as 'configuration/filter' concepts that touch the wire shape. (4) Community 2 (Watcher API & Project Meta) bridges through duplicate representation: AST extracts produce '.UpdateFor*()' nodes in C2 while semantic extracts produce 'Watcher.UpdateFor*' in C3 — MSG shares_data_with the semantic versions, and the AST versions are reachable through Watcher --method--> edges. MSG --references--> Redis Watcher Retro Spec Design also pulls in C2's spec/meta nodes. Contrast with Watcher: Watcher is the behavior-compatibility yardstick (Principle I, Minimal Surface), MSG is the protocol-compatibility yardstick (Principle V, SemVer + wire format). Touching either one shows up immediately as cross-community edge churn.

## Source Nodes

- MSG
- UpdateType
- MSG.MarshalBinary
- MSG.UnmarshalBinary
- Watcher.subscribe
- DefaultUpdateCallback
- FR-Wire