# Hub

個人 vault 入口。一週後檢核這個結構合不合用，不合用就重整。

## 進行中專案
- [[金智官網]] — 智廷工程行官網 SEO 推進中（hub: `10-Projects/金智官網/`）

## 🧠 MOC（領域地圖）
- [[Claude MOC]] — 跟 Claude / AI 開發累積的所有筆記
- [[我的閱讀]] — 在讀 / 讀完 / 棄書
- [[我的觀影]] — 看過的電影

## 🔥 全 vault 未完成待辦（自動）

```dataview
TASK
WHERE !completed AND !contains(file.path, "90-Templates")
GROUP BY file.link
```

## 📅 最近編輯的筆記（自動）

```dataview
TABLE file.mtime AS "最後修改"
FROM ""
WHERE file.name != "Hub"
SORT file.mtime DESC
LIMIT 10
```

## 📂 持續關注（自己加）
- 

## 第二大腦守則
- **Inbox 每週清空**（週日晚 10 分鐘）
- **一個資訊只一個位置**（避免 Notion / Obsidian 同步同一份）
- **寫優於整理**（不知放哪先丟 `00-Inbox/`）
- **Daily Note 每天寫一行也算**（連續比完美重要）

## 一週後回頭做的事
- Inbox 累積了什麼樣的東西？決定該開哪些 `30-Resources/` 子資料夾
- 哪些 prompt 重用過？那時候才建 `30-Resources/claude/prompts/`
- 哪些段落每天都出現在 Daily Note？改範本
