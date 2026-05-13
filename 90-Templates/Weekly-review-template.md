---
created: <% tp.date.now("YYYY-MM-DD HH:mm") %>
tags: [weekly-review]
week: <% tp.date.now("YYYY-[W]ww") %>
---

# 第 <% tp.date.now("ww") %> 週覆盤（<% tp.date.now("YYYY-MM-DD", -6) %> ~ <% tp.date.now("YYYY-MM-DD") %>）

## 📅 本週做了什麼（自動）

### Daily notes 列表
```dataview
LIST
FROM "99-Daily"
WHERE file.cday >= date(today) - dur(7 days)
SORT file.cday ASC
```

### 本週新建的筆記（不含 Daily / Templates）
```dataview
LIST
FROM "" AND -"99-Daily" AND -"90-Templates"
WHERE file.cday >= date(today) - dur(7 days)
SORT file.cday DESC
```

### 本週完成的待辦
```dataview
TASK
WHERE completed AND completion >= date(today) - dur(7 days)
GROUP BY file.link
```

### Inbox 累積（待整理）
```dataview
LIST
FROM "00-Inbox"
```

## 🎯 三件最有 impact 的事
- 
- 
- 

## 💡 本週學到（3 件最重要的）
- 
- 
- 

## 🚧 卡關 / 拖延
- 什麼事一直沒做？
- 為什麼？

## 🔄 系統檢視
- vault 結構還合用嗎？哪個資料夾爆炸了？
- 哪些 wiki link 變孤兒（連結到不存在的檔）？

## ⏭ 下週意圖
- 一件最想推進的：
- 兩個要嘗試的：
- 一個要停止做的：

## 🔗 連結到上週
← [[<% tp.date.now("YYYY-[W]ww", -7) %>|上週覆盤]]
