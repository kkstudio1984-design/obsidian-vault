# 2026-05-31 明天上課版：20 分鐘教會 Web Clipper 到 LLM Wiki

## 課程定位

這是一堂 20 分鐘的短教學，目標不是完整介紹 Obsidian，也不是完整介紹 Codex，而是讓學員完成一個最小閉環：

```text
看到一篇網頁 -> 用 Web Clipper 收進 Obsidian -> 放到 Inbox -> 用 Codex 判斷去向 -> 形成 Wiki / Skill / Output
```

一句話課程承諾：

> 20 分鐘後，你會知道怎麼把網頁資料收進 Obsidian，並讓 AI 幫你把它變成可用知識。

## 適合對象

- 已經聽過 Obsidian，但不知道怎麼開始用的人。
- 常常收藏文章，但之後找不到、用不到的人。
- 想用 AI 整理網頁、文章、影片資料的人。
- 想建立自己的 LLM Wiki，但不想一開始就搭太複雜的人。

## 上課前準備

### 講師準備

- Obsidian 已打開 vault：`Obsidian-vault`
- Vault 中已有資料夾：

```text
00 Inbox 原始資料
10 Wiki 知識庫
20 Skills 方法庫
30 Outputs 輸出
40 Reviews 複盤
90 Index 索引
```

- 瀏覽器已安裝 Obsidian Web Clipper。
- Web Clipper template 已設定：
  - Vault：`Obsidian-vault`
  - Note location：`00 Inbox 原始資料/Web Clipper`
  - Note name：`{{date}} - {{title}}`
- 準備一篇示範網頁，建議用和 AI / Obsidian / 學習方法相關的文章。

### 學員準備

如果是現場一起做，學員需要：

- 已安裝 Obsidian。
- 已安裝 Web Clipper。
- 有一個 Obsidian vault。

如果學員來不及安裝，仍可先看示範，課後再照筆記操作。

---

## 20 分鐘時間表

| 時間 | 段落 | 目的 |
|---|---|---|
| 0:00-2:00 | 痛點開場 | 讓學員知道為什麼要學 |
| 2:00-4:00 | 一張圖講懂 LLM Wiki | 建立整體心智模型 |
| 4:00-7:00 | Web Clipper 設定 | 避免 vault / 路徑錯誤 |
| 7:00-11:00 | 現場剪一篇文章 | 完成第一個輸入 |
| 11:00-15:00 | 用 Codex 整理 Inbox | 示範 AI 如何判斷去向 |
| 15:00-18:00 | 產出 Wiki / Skill / Output | 讓資料變成可用知識 |
| 18:00-20:00 | 收尾與課後任務 | 讓學員知道回去怎麼做 |

---

## 0:00-2:00 痛點開場

### 講師目標

讓學員立刻感覺這堂課和自己有關。

### 講師台詞

> 你有沒有遇過這種狀況：看到一篇好文章，先收藏；看到一段好觀點，先截圖；看到一個工具教學，心想之後一定會用。結果一個月後，這些東西不是找不到，就是找到了也不知道怎麼用。
>
> 今天這 20 分鐘，我們只解決一件事：不要再讓收藏變成雜物堆。我要示範怎麼用 Obsidian Web Clipper 把網頁收進 Inbox，再用 Codex 幫我們判斷它應該變成 Wiki、Skill，還是輸出素材。

### 板書金句

```text
收藏不是知識，整理後能再次使用，才是知識。
```

---

## 2:00-4:00 一張圖講懂 LLM Wiki

### 講師目標

用最短時間讓學員知道整套系統怎麼流動。

### 畫面展示

打開 Obsidian 側邊欄，展示 6 個資料夾。

```text
00 Inbox 原始資料
10 Wiki 知識庫
20 Skills 方法庫
30 Outputs 輸出
40 Reviews 複盤
90 Index 索引
```

### 講師台詞

> 這套系統其實只有一條主線。所有還沒整理的東西，先進 Inbox。整理後，如果它是概念，就進 Wiki；如果它是可重複的方法，就進 Skills；如果它可以變成文章、簡報、報告或專案內容，就進 Outputs。最後每週做一次 Reviews，把有價值的東西回流。

### 一句話解釋每層

- Inbox：先收進來。
- Wiki：整理成知識。
- Skills：整理成方法。
- Outputs：整理成成果。
- Reviews：整理成下一輪改進。
- Index：整理成入口。

---

## 4:00-7:00 Web Clipper 設定

### 講師目標

先避開最常見錯誤：Vault 填成路徑。

### 現場操作

打開 Web Clipper settings → Templates → 選 template。

### 必填欄位

Template name：

```text
LLM Wiki Inbox
```

Behavior：

```text
Create new note
```

Note name：

```text
{{date}} - {{title}}
```

Note location：

```text
00 Inbox 原始資料/Web Clipper
```

Vault：

```text
Obsidian-vault
```

### 講師提醒

> 這裡最容易錯的是 Vault。Vault 要選 Obsidian 裡的 vault 名稱，不是 Windows 路徑。所以要選 `Obsidian-vault`，不要填 `D:\Obsidian-vault`。

### Template content

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

---

## 7:00-11:00 現場剪一篇文章

### 講師目標

讓學員看到資料真的會進 Obsidian。

### 操作步驟

1. 打開一篇示範文章。
2. 點瀏覽器上的 Obsidian Web Clipper。
3. 確認 template 是 `LLM Wiki Inbox`。
4. 確認 vault 是 `Obsidian-vault`。
5. 確認 Note location 是 `00 Inbox 原始資料/Web Clipper`。
6. 按 Add to Obsidian。
7. 回 Obsidian 側邊欄確認檔案出現。

### 講師台詞

> 注意，現在這篇文章只是進入 Inbox，還不是知識。這一步叫輸入，不叫整理。真正的價值是在下一步：讓 Codex 幫我們判斷它該去哪裡。

### 現場檢查

在 Obsidian 打開剛剪下來的筆記，確認有：

- source
- title
- clipped date
- 原文內容
- 初步觀察
- 整理去向

---

## 11:00-15:00 用 Codex 整理 Inbox

### 講師目標

示範 AI 不是只回答問題，而是維護知識庫。

### 給 Codex 的現場指令

```text
請整理「00 Inbox 原始資料/Web Clipper」裡最新剪藏的這篇文章。

請幫我判斷：
1. 這篇文章的核心主題是什麼？
2. 它值得整理到 10 Wiki 知識庫嗎？如果值得，應該建立什麼筆記？
3. 它有沒有可以沉澱成 20 Skills 方法庫的方法或流程？
4. 它能不能變成 30 Outputs 輸出的文章、課程、簡報或專案素材？
5. 請在原始剪藏底部標記整理狀態。
```

### 講師台詞

> 這裡我們不是叫 AI 幫我們「摘要一下」而已。摘要只是第一步。真正重要的是讓 AI 幫我們判斷：這份資料要進 Wiki、變 Skill、變 Output，還是封存。

---

## 15:00-18:00 產出 Wiki / Skill / Output

### 講師目標

讓學員看到資料從收藏變成可用成果。

### 三種可能產出

#### 1. 變成 Wiki

適合：概念、原理、比較、來源摘要。

範例：

```text
10 Wiki 知識庫/來源摘要/文章標題.md
```

#### 2. 變成 Skill

適合：重複流程、提示詞、SOP、檢查清單。

範例：

```text
20 Skills 方法庫/某某流程 Skill.md
```

#### 3. 變成 Output

適合：文章、課程、簡報、專案文件。

範例：

```text
30 Outputs 輸出/教學/某某教學.md
```

### 講師台詞

> 判斷一份資料的價值，不是看它有多長，而是看它能不能再次使用。能解釋世界的，進 Wiki；能重複操作的，進 Skill；能對外交付的，進 Output。

---

## 18:00-20:00 收尾與課後任務

### 三句總結

1. Web Clipper 負責輸入，不負責整理。
2. Inbox 是暫存區，不是知識庫。
3. Codex 的價值是幫你把資料判斷去向，讓知識流動。

### 課後任務

請學員回去完成：

1. 用 Web Clipper 剪 3 篇真正會用到的文章。
2. 全部放進 `00 Inbox 原始資料/Web Clipper`。
3. 請 Codex 整理這 3 篇，至少產出：
   - 1 篇 Wiki 筆記
   - 1 個 Skill 或整理流程
   - 1 個可輸出的題目

### 課後指令

```text
請整理我今天用 Web Clipper 收進「00 Inbox 原始資料/Web Clipper」的 3 篇文章。

請幫我：
1. 列出每篇文章的主題與價值。
2. 選出最值得進 Wiki 的內容，建立一篇 Wiki 筆記。
3. 找出可以沉澱成 Skill 的流程。
4. 找出可以變成 Output 的文章、課程、簡報或專案素材。
5. 在每篇原始剪藏底部標記整理狀態。
```

---

## 明天講師備忘

### 最重要的教學取捨

20 分鐘不要教太多。明天只要讓學員理解並完成這條線：

```text
網頁 -> Web Clipper -> Inbox -> Codex -> Wiki / Skill / Output
```

不要展開講：

- 太多 Obsidian 外掛
- 太多 AI model 設定
- 太多自動化
- 太多知識管理理論

### 現場常見問題

#### Q：為什麼剪藏後跳出 Vault not found？

A：Vault 欄位要選 vault 名稱 `Obsidian-vault`，不是路徑 `D:\Obsidian-vault`。

#### Q：可以直接剪到 Wiki 嗎？

A：不建議。剪藏是原始資料，先進 Inbox，整理後再進 Wiki。

#### Q：如果文章格式很亂怎麼辦？

A：先用 Reader mode，或只選取重要段落再剪藏。

#### Q：一定要每篇都整理嗎？

A：不用。Inbox 的目的就是先收，週末再篩選。低價值內容可以封存。

### 明天現場金句

> 不要讓 AI 幫你收藏更多東西，要讓 AI 幫你判斷什麼值得留下。

> Inbox 是入口，不是終點。

> 能解釋世界的進 Wiki，能重複操作的進 Skill，能對外交付的進 Output。