# Obsidian Web Clipper 教學

## 課程目標

這份教學會帶你把 Obsidian Web Clipper 接進目前的 LLM Wiki 流程，讓網頁資料先進入 `00 Inbox 原始資料`，再由 Codex 定期整理到 Wiki、Skills 或 Outputs。

適合目標：

- 快速收藏文章、網頁、影片頁面、工具文件。
- 保存選取文字或重點 highlight。
- 把網頁內容轉成 Markdown 筆記。
- 讓剪藏資料進入 LLM Wiki 的知識循環。

## Web Clipper 是什麼

Obsidian Web Clipper 是 Obsidian 官方的瀏覽器擴充功能，可以在瀏覽器中擷取網頁內容，並保存到你的 Obsidian vault。

它支援：

- 擷取整個網頁或主要文章內容。
- 擷取你選取的文字。
- Highlight 網頁重點後再保存。
- Reader mode，先把頁面轉成乾淨閱讀版再保存。
- Templates，設定不同網站或內容類型的儲存格式。
- Variables / filters，把標題、網址、作者、日期等 metadata 自動寫進筆記。

官方說明也提到，剪藏內容會保存到本地 Obsidian vault，且不收集使用資料。

## 安裝

到官方 Web Clipper 頁面安裝對應瀏覽器版本：

- Chrome / Brave / Arc / Chromium：Chrome Web Store
- Firefox：Firefox Add-ons
- Safari：Safari Extensions
- Edge：Microsoft Edge Add-ons

官方入口：

https://obsidian.md/clipper

安裝後，瀏覽器工具列會出現 Obsidian 圖示。

## 第一次設定

### 1. 開啟 Clipper

在任一網頁按瀏覽器上的 Obsidian 圖示。

也可以用快捷鍵：

- Windows / Linux：`Ctrl + Shift + O`
- macOS：`Cmd + Shift + O`

### 2. 選擇 vault

在 Clipper 底部選擇目前使用的 vault：

```text
D:\Obsidian-vault
```

如果看不到 vault，先確認 Obsidian 已經開過這個 vault，並允許瀏覽器開啟 Obsidian protocol。

### 3. 設定預設儲存資料夾

建議先把剪藏內容全部放進：

```text
00 Inbox 原始資料/Web Clipper
```

原因：Web Clipper 是輸入工具，不要一開始就把剪藏內容直接塞進 Wiki。先進 Inbox，之後再由 Codex 幫你整理，會比較乾淨。

## 基本使用流程

### 情境 A：收藏整篇文章

1. 打開文章頁面。
2. 點瀏覽器上的 Obsidian Web Clipper 圖示。
3. 確認預覽內容。
4. Folder 選 `00 Inbox 原始資料/Web Clipper`。
5. 按 `Add to Obsidian`。

適合：長文章、官方文件、教學文、部落格。

### 情境 B：只保存選取文字

1. 在網頁上選取一段文字。
2. 打開 Web Clipper。
3. Clipper 會優先使用選取內容。
4. 按 `Add to Obsidian`。

適合：只想保存一段觀點，不想整篇收藏。

### 情境 C：Highlight 後保存

1. 打開 Web Clipper。
2. 開啟 Highlighter。
3. 在網頁上標記重要文字、圖片或區塊。
4. 再次打開 Clipper。
5. 保存 highlights。

官方文件提到，highlights 可以加入筆記內容，也可以取代原文內容，或只保留原始內容不插入 highlight。

適合：讀文章時邊看邊畫重點。

### 情境 D：Reader mode 再剪藏

1. 打開 Web Clipper。
2. 點 Reader。
3. 檢查乾淨版文章內容。
4. 按 `Add to Obsidian`。

適合：廣告很多、版面混亂、側欄很多的頁面。

## 建議模板：LLM Wiki Inbox 剪藏模板

在 Web Clipper 設定中建立新 template：

Template name：

```text
LLM Wiki Inbox
```

Behavior：

```text
Create a new note
```

Note location：

```text
00 Inbox 原始資料/Web Clipper
```

Note name：

```text
{{date}} - {{title}}
```

Template content：

```markdown
---
source: {{url}}
title: {{title}}
author: {{author}}
published: {{published}}
clipped: {{date}}
tags:
  - inbox
  - web-clipper
status: 未整理
---

# {{title}}

來源：{{url}}

## 原文內容

{{content}}

## 初步觀察

- 這篇內容主要在說什麼？
- 哪些觀點值得整理到 Wiki？
- 是否有可以沉澱成 Skill 的流程？
- 是否可以變成文章、課程、報告或專案素材？

## 整理去向

- [ ] 10 Wiki 知識庫
- [ ] 20 Skills 方法庫
- [ ] 30 Outputs 輸出
- [ ] 40 Reviews 複盤/Archives
```

## 進階模板：只保存 Highlights

如果你習慣只收重點，可以建立另一個 template：

Template name：

```text
LLM Wiki Highlights
```

Note location：

```text
00 Inbox 原始資料/Web Clipper Highlights
```

Template content：

```markdown
---
source: {{url}}
title: {{title}}
clipped: {{date}}
tags:
  - inbox
  - highlights
status: 未整理
---

# {{title}}

來源：{{url}}

## Highlights

{{highlights}}

## 我的判斷

- 最重要的 1 個觀點：
- 可以連到哪個主題：
- 下一步：
```

## 和 LLM Wiki 的搭配方式

Web Clipper 不負責整理，它只負責「低摩擦輸入」。

推薦流程：

```text
網頁 / 文章 / 文件
        ↓
Obsidian Web Clipper
        ↓
00 Inbox 原始資料/Web Clipper
        ↓
Codex 每週整理
        ↓
10 Wiki 知識庫 / 20 Skills 方法庫 / 30 Outputs 輸出
```


## 五大常用情境

### 1. 學習筆記：把教學文章變成可複習材料

適合內容：

- 工具教學
- 技術文章
- 線上課程頁面
- 讀書心得
- 方法論文章

使用方式：

1. 打開教學文章。
2. 使用 Reader mode 清理頁面。
3. 用 `LLM Wiki Inbox` template 剪到 `00 Inbox 原始資料/Web Clipper`。
4. 週末請 Codex 整理成 Wiki 筆記。

整理後去向：

- `10 Wiki 知識庫/概念`
- `20 Skills 方法庫`

範例指令：

```text
請把這篇 Web Clipper 剪下來的教學文章整理成學習筆記，包含核心概念、操作步驟、常見錯誤和可複用模板。
```

### 2. 主題研究：收集多篇資料後做比較分析

適合內容：

- 同一主題的多篇文章
- 官方文件
- 評測文
- Reddit / GitHub / blog 討論
- 不同工具比較

使用方式：

1. 對同一主題剪 3-5 篇資料。
2. 每篇都保留 source URL。
3. 統一放進 `00 Inbox 原始資料/Web Clipper/主題名稱`。
4. 請 Codex 做比較整理。

整理後去向：

- `10 Wiki 知識庫/比較分析`
- `30 Outputs 輸出/報告`

範例指令：

```text
請比較 Web Clipper 中這 5 篇關於同一主題的資料，整理共同觀點、分歧觀點、可信來源、可行結論，並建立一份比較分析筆記。
```

### 3. 內容創作：把素材累積成文章或腳本

適合內容：

- 金句
- 案例
- 數據
- 故事
- 社群貼文
- 競品內容

使用方式：

1. 看到有用素材時，只剪選取文字或 highlights。
2. 用 `LLM Wiki Highlights` template 保存。
3. 在筆記中補一句「我可能怎麼用」。
4. 寫作時請 Codex 從素材庫中找可用片段。

整理後去向：

- `30 Outputs 輸出/文章`
- `30 Outputs 輸出/腳本`
- `20 Skills 方法庫/寫作`

範例指令：

```text
請從最近 Web Clipper 收集的素材中，找出可以用來寫一篇文章的觀點、案例和開頭鉤子，並產出一份文章大綱。
```

### 4. 專案資料：把參考資料集中到專案輸出裡

適合內容：

- 客戶網站參考
- 競品頁面
- 設計案例
- 技術文件
- SEO 文章
- 產品說明頁

使用方式：

1. 剪藏時在標題加上專案名稱。
2. 先放 Inbox，不急著放進專案資料夾。
3. 請 Codex 判斷哪些資料應該回流到專案。
4. 有價值的內容再整理到 `30 Outputs 輸出/Projects/專案名稱`。

整理後去向：

- `30 Outputs 輸出/Projects`
- `10 Wiki 知識庫/Resources`
- `20 Skills 方法庫/專案流程`

範例指令：

```text
請整理 Web Clipper 中和「金智官網」相關的剪藏資料，判斷哪些可以作為網站架構、SEO、案例頁、服務頁或視覺參考，並整理到專案資料夾。
```

### 5. 靈感收集：快速捕捉短觀點，週末再整理

適合內容：

- 突然看到的一句話
- 社群觀點
- 產品想法
- 工作方法
- 生活洞察
- 想之後再研究的線索

使用方式：

1. 不剪整篇，只剪重點段落。
2. 用 highlights 或選取文字保存。
3. 在筆記底部補一句「為什麼我覺得它有用」。
4. 週複盤時再決定保留、整理或封存。

整理後去向：

- `00 Inbox 原始資料/Web Clipper Highlights`
- `10 Wiki 知識庫/概念`
- `40 Reviews 複盤`

範例指令：

```text
請整理這週 Web Clipper Highlights 中的靈感片段，分成值得沉澱、可以延後、應該封存三類，並找出 3 個最值得下週追蹤的主題。
```

## 五大情境對照表

| 情境 | 最適合剪什麼 | 儲存位置 | 後續去向 |
|---|---|---|---|
| 學習筆記 | 教學文、方法論、課程頁 | `00 Inbox 原始資料/Web Clipper` | Wiki / Skills |
| 主題研究 | 多篇同主題資料 | `00 Inbox 原始資料/Web Clipper/主題` | Wiki 比較分析 / Outputs 報告 |
| 內容創作 | 金句、案例、數據、故事 | `00 Inbox 原始資料/Web Clipper Highlights` | Outputs 文章 / 腳本 |
| 專案資料 | 競品、案例、文件、參考頁 | `00 Inbox 原始資料/Web Clipper/專案` | Outputs Projects / Wiki Resources |
| 靈感收集 | 短觀點、想法、線索 | `00 Inbox 原始資料/Web Clipper Highlights` | Reviews / Wiki 概念 |

## 每週整理指令

當 Web Clipper 裡累積一些內容後，可以請 Codex 整理：

```text
請整理「00 Inbox 原始資料/Web Clipper」裡尚未整理的剪藏資料。

請幫我：

1. 列出本週新增剪藏。
2. 判斷每篇內容的主題與價值。
3. 找出值得整理到「10 Wiki 知識庫」的概念。
4. 找出可以沉澱到「20 Skills 方法庫」的方法或流程。
5. 找出可以變成「30 Outputs 輸出」的文章、課程、報告或專案素材。
6. 對低價值或重複內容，建議封存到「40 Reviews 複盤/Archives」。
```

## 使用習慣建議

### 不要什麼都剪

剪藏前先問：

- 我未來真的會用到嗎？
- 它能補強哪個主題？
- 它能變成觀點、方法或素材嗎？

### 剪藏後不要馬上整理

先進 Inbox，週末再集中整理。這樣不會打斷閱讀和工作節奏。

### 優先保存「可再使用」的內容

值得剪：

- 方法論
- 案例
- 數據
- 工具教學
- 寫作素材
- 專案參考

比較不值得剪：

- 只是當下有趣但無法再用的內容
- 沒有來源或可信度不明的資訊
- 和目前目標完全無關的文章

## 常見問題

### Q1：為什麼剪藏後看不到？

檢查：

- Clipper 選到的 vault 是否是 `D:\Obsidian-vault`。
- Folder 是否填對。
- Obsidian 是否允許瀏覽器開啟 Obsidian protocol。
- Obsidian 是否需要重新整理。

### Q2：為什麼內容格式很亂？

試試：

- 使用 Reader mode。
- 改用選取文字剪藏。
- 建立特定網站 template。
- 只保存 highlights。

### Q3：要直接剪到 Wiki 嗎？

不建議。

Web Clipper 是輸入工具，剪下來的內容還沒消化。先放 `00 Inbox 原始資料`，等 Codex 或週複盤整理後，再進 Wiki。

## 最小可行練習

今天先做三件事：

1. 安裝 Obsidian Web Clipper。
2. 建立 `LLM Wiki Inbox` template。
3. 剪 3 篇你最近真的會用到的文章到 `00 Inbox 原始資料/Web Clipper`。

然後用 Codex 跑一次：

```text
請整理我剛剛用 Web Clipper 收進 Inbox 的 3 篇文章，幫我判斷哪些該進 Wiki、哪些可以變成 Skill、哪些可以做成 Output。
```

## 參考來源

- Obsidian Web Clipper 官方頁：https://obsidian.md/clipper
- Obsidian Web Clipper 官方說明：https://obsidian.md/help/web-clipper
- Clip web pages 官方說明：https://obsidian.md/help/web-clipper/capture
- Highlighter 官方說明：https://obsidian.md/help/web-clipper/highlight
- Templates 官方說明：https://obsidian.md/help/web-clipper/templates