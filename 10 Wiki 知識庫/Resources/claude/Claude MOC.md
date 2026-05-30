---
created: 2026-05-13
tags: [moc, claude]
---

# Claude MOC（Map of Content）

跟 Claude / AI 開發相關的所有筆記入口。MOC 不是清單而是地圖 — 你的思考路徑紀錄。

## 🧠 跨專案累積的智慧
這是這個 vault 最重要的部分。每次踩過 Claude 的雷或學到新工法，寫一篇進來。

```dataview
LIST
FROM "30-Resources/claude/learnings"
SORT file.ctime DESC
```

## 📝 提示詞庫
重複用得到的 prompt。建立判準：用過 2 次以上才放這。

```dataview
LIST
FROM "30-Resources/claude/prompts"
SORT file.mtime DESC
```

（目前空 — 等你有重用 3 次以上的 prompt 再加）

## 💬 重要對話存檔
完成過的高價值 Claude 對話。建立判準：6 個月後翻回來還有價值。

```dataview
LIST
FROM "30-Resources/claude/conversations"
SORT file.ctime DESC
```

（目前空 — 等真的有值得存的對話再加）

## 🔗 相關專案
- [[金智官網]] — 今天用 Claude 完成大量 SEO 推進
- （未來其他專案）

## 📚 自己的 Claude 操作守則
- vault 根目錄的 `CLAUDE.md` — Claude Code 在 vault 內活動時的指引
- 全域記憶 在 `C:\Users\USER\.claude\projects\.../memory/`
