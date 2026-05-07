# 專案檔案結構與用途註解(2026-05-06 snapshot)

本檔案對應 `tree` 命令在 `fork260506-redis-watcher/` 根目錄的輸出,
為每個檔案/目錄補上一行用途註解,作為閱讀程式碼前的索引。

- 命名沿用 `x_fork.graphify-20260506.md` 的「snapshot 日期」慣例。
- `graphify-out/` 整個目錄由工具自動生成(78 檔中佔大宗),於目錄層級
  一句話帶過,不展開內部結構。
- 其餘 Go 原始碼、設定、文件每一檔都附註解。

```
.
├── CLAUDE.md                       # 給 Claude Code 看的專案指令(graphify 規則:回答架構問題前先讀 GRAPH_REPORT.md;改碼後跑 graphify update .)
├── LICENSE                         # Apache 2.0 授權(承自 upstream casbin/redis-watcher,fork 不得改授權)
├── README.md                       # 公開 README(Casbin Redis Watcher 簡介 + 最小 example;example 仍引用 go-redis/redis/v8,屬已知技術債)
│
├── docs/                           # 文件目錄(snapshot 時尚未 commit,untracked 狀態)
│   └── superpowers/
│       └── specs/
│           └── 2026-05-07-redis-watcher-retro-spec-design.md   # superpowers brainstorming 產出的 retro spec 設計文件(尚未轉成 specs/001-retro-spec/spec.md)
│
├── examples/                       # Casbin 範例資料(README 與 watcher_test.go 共用)
│   ├── rbac_model.conf             # RBAC 模型定義(Casbin model 語法)
│   └── rbac_policy.csv             # RBAC 政策資料(p, g 行)
│
├── go.mod                          # Go module 宣告(module = github.com/go-admin-team/redis-watcher/v2,Go 1.20;直依 casbin/v2、redis/go-redis/v9、google/uuid)
├── go.sum                          # Go module 校驗碼(go mod tidy 自動維護)
│
├── graphify-out/                   # graphify 知識圖譜輸出(整個目錄由工具生成,可由 graphify update . 重建;內含 GRAPH_REPORT.md、Obsidian vault、互動 HTML、原始 graph.json 等)
│
├── options.go                      # 套件原始碼:WatcherOptions struct(Channel/IgnoreSelf/LocalID/SubClient/PubClient/OptionalUpdateCallback)+ package-level initConfig 補預設值
├── watcher.go                      # 套件原始碼:Watcher struct、三個 New* 構造器、九個 Update* 公開方法、subscribe/Close 流程、MSG 與 UpdateType 定義、DefaultUpdateCallback dispatch
├── watcher_test.go                 # 測試原始碼:涵蓋 watcher 構造、IgnoreSelf 兩種模式、九種 UpdateType 對應的 publish/subscribe flow
│
├── x_fork.branch-origin.md         # fork 由來說明(2026-05-06 從 master 拉出 main、保留 master 不動、不 squash/rebase)
└── x_fork.graphify-20260506.md     # graphify session 紀錄(2026-05-06 本次 fork 生圖譜的過程)
```

---

## 補充說明

**幾個重要慣例**:

- 整個 fork 只有一個 Go 套件:`rediswatcher`(套件根 = repo 根)。沒有
  子目錄子套件,沒有 internal/、pkg/、cmd/ 分層。
- `*_test.go` 是 Go 標準測試檔;本 repo 全部測試集中在 `watcher_test.go`。
- Functional options pattern 在這裡退化成「struct + 公開欄位」(`WatcherOptions`),
  不是 `WithXxx(...) Option` 那種 callback 風格 —— 上游就這麼設計,fork 沿用。
- `x_fork.*` 開頭的檔案都是這份個人 fork 的 meta 紀錄,不影響任何程式邏輯,
  可安全忽略或刪除(對應 `x_fork.branch-origin.md` 的尾註)。
- README.md 的 example 與實際匯入的 redis client 不一致(README 寫
  `go-redis/redis/v8`,程式碼用 `redis/go-redis/v9`)—— 已在 constitution
  v1.0.0 的 Technology & Compatibility Constraints 段標注為已知技術債。

**最常被引用的 god nodes**(來自 graphify `GRAPH_REPORT.md`):

| 節點 | 所在檔案 | 邊數 |
|---|---|---|
| `Watcher` | `watcher.go` | 17 |
| `initWatcherWithOptions()` | `watcher_test.go` | 16 |
| `Redis Watcher` | `README.md`(概念節點) | 9 |
| `TestUpdate()` | `watcher_test.go` | 6 |
| `TestWatcher()` | `watcher_test.go` | 5 |
| `TestWatcherWithIngnoreSelfFalse()` | `watcher_test.go` | 5 |
| `TestWatcherWithIgnoreSelfTrue()` | `watcher_test.go` | 5 |
| `miso168net/fork260506-redis-watcher` | `x_fork.branch-origin.md`(provenance 節點) | 5 |
| `NewWatcher()` | `watcher.go` | 4 |
| `NewWatcherWithCluster()` | `watcher.go` | 4 |

讀程式碼建議從 `Watcher` struct 與 `initWatcherWithOptions()` 入口往外爬,
測試端與實作端都會帶到,效率最高。

---

*本檔案於 2026-05-08 由 Claude Code 依 `tree` 輸出生成,日期 `20260506`
沿用 fork 的 snapshot 命名慣例(對齊 `x_fork.graphify-20260506.md`)。*
