# Jev 生態實地指南

[English](README.md) · 繁體中文

Jev（TypeSafe System One）周邊值得裝的東西，一份帶查證的清單。

**這裡只有知識，沒有程式。** 本機自己的實作在
[royalskynet/jev-gate-mcp](https://github.com/royalskynet/jev-gate-mcp)，
那個 repo 只收跟該工具有關的內容。

## 清單（2026-09-22 查證）

星數與最後 push 由 `gh api graphql` 當日抓取，非轉述。12 個全部存在、
皆未封存（`isArchived: false`）。

| # | repo | ★ | 最後 push | 它是什麼（作者原述） |
|---|---|---|---|---|
| 1 | [browser-use/jev-ultrafast](https://github.com/browser-use/jev-ultrafast) | 16,901 | 09-18 | 最快也最便宜的網頁 agent |
| 2 | [vercel-labs/json-render](https://github.com/vercel-labs/json-render) | 18,001 | 09-21 | 生成式 UI 框架 |
| 3 | [tamaratran/fast-jev-compaction](https://github.com/tamaratran/fast-jev-compaction) | 6,112 | 09-18 | Claude Code plugin：用 Jev 判斷取代壓縮摘要，每個 tool call 與結果一次評分，過期的丟掉或截斷，留下的逐字保留 |
| 4 | [lahfir/agent-desktop](https://github.com/lahfir/agent-desktop) | 1,451 | 09-21 | Rust 寫的桌面控制，讀 OS 無障礙樹拿真實 UI 結構，ref 穩定、動作可安全重試，不靠像素猜 |
| 5 | [devagrawal09/jev-review](https://github.com/devagrawal09/jev-review) | 514 | 09-17 | 分階段的 code review 工作流與本機 dashboard |
| 6 | [itsmostafa/typesafe-mcp](https://github.com/itsmostafa/typesafe-mcp) | 238 | 09-21 | MCP connector，讓 agent 直接用 TypeSafe 的 Jev 模型 |
| 7 | [jkudish/jev-mcp](https://github.com/jkudish/jev-mcp) | 257 | 09-21 | 把 Jev 的快速、便宜、typed 判斷包成 MCP tools |
| 8 | [0xNatoshi/jev-codex-router](https://github.com/0xNatoshi/jev-codex-router) | 189 | 09-22 | Codex 的每輪模型／推理路由，由 Jev 決定模型、思考深度與速度模式 |
| 9 | [GhalebDweikat/winnow](https://github.com/GhalebDweikat/winnow) | 60 | 09-19 | Claude Code 的校準過的 context 篩子：每個 tool 結果進 context 前先被 System One 模型判一次 |
| 10 | [jarrodwatts/jev-trader](https://github.com/jarrodwatts/jev-trader) | 1,921 | 09-17 | 每個 Monad block 一次 AI 交易決策 |
| 11 | [fhshaik/typesafe-mario](https://github.com/fhshaik/typesafe-mario) | 343 | 09-16 | 從結構化的模擬器狀態打 Super Mario Bros. |
| 12 | [monteduro/killmyidea](https://github.com/monteduro/killmyidea) | 81 | 09-18 | 描述你的點子，Jev 判 kill / fix / ship |

## 宣稱 vs 實測

流傳的推薦文帶了一串數字——7 秒跑完航班搜尋、81 毫秒決策延遲、砍掉約 60% 帳單、
237 輪測試回放。**那些是作者或轉述者的宣稱，本清單沒有複現過任何一項。**
查證到的只有上表：repo 存在、活著、星數與最後 push 是那天的值。

本機真的量過的只有兩件事，數據在 jev-gate-mcp 的 DEVLOG：

- **#3 fast-jev-compaction**：實裝在用。壓縮實測見 DEVLOG §21。
- **#9 winnow 的同領域**：本機自己的 `hooks/jev.js` prune 做同一件事。真實 ledger
  19 次呼叫只有 1 次剪到東西（一包 44 KB Bash 輸出，省 28,015 字元），
  其餘 18 次含三次 12–13 KB 的 Read 一行都沒剪。所以「每個 tool 結果都先判一次」
  聽起來划算，實際上**門檻設在哪比判得多準更決定效益**——低於一個 chunk 的輸出，
  題目退化成整包丟或整包留，判官理所當然答留。細節見 jev-gate-mcp README 的門檻表。

裝之前值得先問的一句：**這個工具在哪個量級才回本**。上面兩個案例都指向同一件事，
省下來的不是「判得準」，是「該判的才判」。

## 最小上手閉環

原推薦文的建議：先看 1 摸機制 → 裝 6 接協議 → 3 壓 context → 5 排雷。

本機實際採用的路徑不同，記在這裡當對照：先 6（`typesafe-mcp` 拿到原語）
→ 3（compaction，是唯一一個裝了立刻有感的）→ 自己寫 prune hook（等同 9 的位置，
因為要控門檻）。1、10、11 是 demo 性質，看機制用，不進日常。

## 範圍

這個 repo 只放清單、查證與取捨理由。任何一個工具的實作、設定或除錯記錄，
放到那個工具自己的 repo，不往這裡抄。
