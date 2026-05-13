# Obsidian Vault — Claude Code 操作守則

當 Claude Code 在這個 vault 內被叫起來時，依以下原則協助。

## Vault 結構（PARA 改編）

```
00-Inbox/        # 收件匣，未整理
10-Projects/     # 進行中專案（有 deadline）
20-Areas/        # 持續關注領域（無 deadline）
30-Resources/    # 參考素材、學習筆記、prompt 庫
40-Archives/     # 結案歸檔
90-Templates/    # 範本（Templater 用 EJS 語法 `<% ... %>`）
99-Daily/        # 每日日記
```

## 寫筆記的偏好

- **wikilink 優先**：`[[檔名]]` 而非 `[檔名](path.md)`
- **檔名語意**：中文檔名 OK，但避免特殊字元 `/ \ : * ? " < > |`
- **frontmatter**：所有非臨時筆記至少含 `tags`，方便 Dataview 查
- **不要重新組織既有檔**：除非使用者明說，否則保留現有 folder 位置
- **不要建空 .md 檔**：只在有實質內容時建立

## 知道使用者背景

- 跨多個專案：金智官網（智廷工程行）、Readmoo、其他副案
- 偏好：先動起來、不過度規劃、單向資訊流（避免兩處同步）
- 詳細個人背景參考全域 memory（在 `C:\Users\USER\.claude\projects\.../memory/`）

## 三類常見動作

### A. 「幫我把 X 寫成筆記」
- 預設位置：`00-Inbox/` 或 `30-Resources/`
- 含 frontmatter `created`, `tags`
- 不要在不確定時自動歸檔到 10/20，保留 inbox

### B. 「把 X 連到 Y」
- 用 wikilink；如果目標檔不存在先確認再建
- 不要建一堆假連結污染圖譜

### C. 「整理 inbox」
- 每篇看內容判斷：歸 Projects / Areas / Resources / 刪除
- 如果不確定，標 `status: needs-review` 留在 inbox
- **絕不擅自刪除筆記，除非明確是 placeholder**

## Git 同步

vault 是 git repo（origin: github.com/kkstudio1984-design/obsidian-vault）。
- 不要每次小改就 commit — 由使用者明說
- 例外：批次新增 5+ 檔時可主動建議 commit
