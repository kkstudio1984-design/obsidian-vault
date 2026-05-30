# Karpathy LLM Wiki 知識系統實踐：基礎安裝與建置篇

來源：<https://kenming.idv.tw/karpathy-llm-wiki-fundamental/>  
原始剪藏：[[Karpathy LLM Wiki 知識系統實踐：基礎安裝與建置篇]]  
整理日期：2026-05-30  
狀態：已整理

## 一句話摘要

這篇文章把 Karpathy 的 LLM Wiki 想法落到實作層：用 Obsidian 當 Wiki 介面、用 LLM Agent 當維護者、用 Web Clipper 和 raw 資料夾當輸入層，再透過 ingest、query、lint 等流程讓知識庫持續演化。

## 核心觀點

### 1. Obsidian 是 IDE，LLM 是 programmer，Wiki 是 codebase

文章引用 Karpathy 的比喻：

```text
Obsidian is the IDE; the LLM is the programmer; the wiki is the codebase.
```

這個比喻很重要，因為它把知識庫從「筆記倉庫」轉成「可維護的系統」。

在這個模型裡：

- Obsidian：負責呈現、連結、瀏覽 Markdown。
- LLM Agent：負責讀取、整理、重構、補連結。
- Wiki：是被持續維護的知識 codebase。

### 2. raw 和 wiki 要分層

文章強調 raw/source 和 wiki 不能混在一起。

```text
raw/  -> 原始資料來源
wiki/ -> LLM 消化後的知識層
```

這對目前 vault 的啟發是：

```text
00 Inbox 原始資料 -> 10 Wiki 知識庫
```

Web Clipper 剪下來的內容不應該直接進 Wiki，而應該先進 Inbox，之後再由 Codex 整理。

### 3. LLM Wiki 需要 schema 或 agent 指令

文章提到 `AGENTS.md`、`CLAUDE.md` 這類檔案的作用：讓 LLM Agent 知道這個知識庫的結構、命名規則、整理方式與操作流程。

這對目前 vault 的啟發是：

- `90 Index 索引` 是人類入口。
- `20 Skills 方法庫` 是可操作流程。
- 未來可以建立一份 `CLAUDE.md` 或 `AGENTS.md` 風格的 vault 操作規格。

### 4. 需要 ingest、query、lint 三種操作

文章把 LLM Wiki 的操作拆成：

- ingest：把 raw 資料整理進 wiki。
- query：用 wiki 回答問題或產出內容。
- lint：檢查 wiki 的重複、斷鏈、過時與結構問題。

對應到目前 vault：

| 操作 | 目前對應 |
|---|---|
| ingest | [[Inbox 資料整理 Skill]] |
| query | 從 Wiki / Skills 產出 Outputs |
| lint | [[每週知識庫複盤 Skill]] |

### 5. index 和 log 很重要

文章建議知識庫要有 `index.md` 與 `log.md`。

目前 vault 已有：

- `90 Index 索引`：入口與地圖。
- `40 Reviews 複盤`：類似 log，記錄每次整理與決策。

## 可整併到目前系統的做法

### 已採用

- 用 `00 Inbox 原始資料` 對應 raw。
- 用 `10 Wiki 知識庫` 對應 wiki。
- 用 `20 Skills 方法庫` 存放操作流程。
- 用 `90 Index 索引` 當入口。
- 用 `40 Reviews 複盤` 記錄整理紀錄。

### 建議補強

1. 建立 vault 操作規格，類似 `AGENTS.md`。
2. 建立固定的來源摘要模板。
3. 每週執行一次 lint，也就是檢查重複、斷鏈、過時、未整理內容。
4. 將 Web Clipper 剪藏統一進 Inbox，避免 `Clippings` 散落在根目錄。

## 可行動結論

這篇文章最值得保留的不是工具安裝細節，而是四個系統原則：

1. 原始資料和整理後知識要分層。
2. LLM 需要明確的操作規格。
3. 知識庫要有 ingest / query / lint 三種操作。
4. index 和 log 是知識庫能長期維護的關鍵。

## 相關筆記

- [[LLM Wiki 自生長知識庫]]
- [[Obsidian Web Clipper 作為 LLM Wiki 輸入層]]
- [[知識庫營運總流程 Skill]]
- [[每週知識庫複盤 Skill]]