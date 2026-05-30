---
created: 2026-05-13
tags: [claude-learning, notion, workflow]
related: [[金智官網]]
---

# `@tryfabric/martian` 把 markdown 轉 Notion blocks，比手寫省 90% 工

## 情境
在 [[金智官網]] 專案，要把多份 markdown 文件（手冊、教學、案例）推到 Notion 父頁面。

## 之前的痛
原本想法是用 `@notionhq/client` 一個一個 block 手刻：heading、paragraph、table、code block 各自寫 builder。光是 table 的 `table_row` + cells 結構就難搞。

## 後來的做法

```js
import { markdownToBlocks } from '@tryfabric/martian';
import { Client } from '@notionhq/client';

const md = await readFile('xxx.md', 'utf-8');
const blocks = markdownToBlocks(md);  // 一行轉換完成

await notion.pages.create({
  parent: { type: 'page_id', page_id: PARENT },
  properties: { title: ... },
  children: blocks.slice(0, 100),  // Notion 一次最多 100 個 children
});
// 超過 100 用 blocks.children.append 分批
```

## 重點細節
- `npm install --no-save @tryfabric/martian` 不污染 package.json
- 處理超過 100 blocks 要分批 append
- markdown 內 `[text](D:\path)` 會被 Notion 拒（要 http/https URL），改成 `\`code\`` 即可

## 適用情境
- 跨專案：所有 markdown → Notion 同步都吃這套
- 反向：notion-to-md 已內建在 Next.js 專案，互相搭配

## 反向案例
更新既有 Notion 頁面：先 list children → 一個個 archive → 再 append 新 blocks。31 個 blocks 沒 rate limit 問題。
