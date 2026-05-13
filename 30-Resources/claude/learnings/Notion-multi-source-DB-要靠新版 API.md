---
created: 2026-05-13
tags: [claude-learning, notion, api]
related: [[金智官網]]
---

# Notion multi-source DB 要靠 `Notion-Version: 2025-09-03` API

## 情境
[[金智官網]] 要從一個 DB 搬 8 篇文章到另一個 DB，但新版 DB 用標準 `databases/{id}/query` 一直回：

```
Database with ID xxx does not contain any data sources accessible by this API bot.
```

## 原因
Notion 2025 推出的「multi-source database」結構，DB 是容器，內含一或多個 `data_source`。傳統 API 假設 DB = 單一 data source，新 DB 要走 data source ID。

## 解法

```js
// 1. 用新版 API 列 integration 可看到的 data sources
const r = await fetch('https://api.notion.com/v1/search', {
  method: 'POST',
  headers: {
    Authorization: `Bearer ${TOKEN}`,
    'Content-Type': 'application/json',
    'Notion-Version': '2025-09-03',
  },
  body: JSON.stringify({
    filter: { value: 'data_source', property: 'object' },
  }),
});
// 拿到 data_source_id

// 2. Query 用 data source endpoint（不是 databases）
await fetch(`https://api.notion.com/v1/data_sources/${dsId}/query`, {
  method: 'POST',
  headers: { ..., 'Notion-Version': '2025-09-03' },
  body: JSON.stringify({ page_size: 100 }),
});
```

## 重點
- `@notionhq/client` SDK 預設用舊版 API，新 DB 一定要用 raw fetch
- 整合 connection 要加在**內嵌 DB 本身**，加在父頁面不會自動繼承給 data source
- search 用 `filter: { value: 'data_source', property: 'object' }` 才能列出 data sources（預設只列 databases / pages）

## 兼容性
新 DB 跟舊 DB schema 不同（例如「內容類型」vs「內容類別」），搬遷時需要 property mapping。
