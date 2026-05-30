---
created: 2026-05-13
tags: [claude-learning, git, workflow]
related: [[金智官網]]
---

# PR 小單位拆，比一次大 PR 容易合

## 情境
[[金智官網]] 一天內推進 10 個 PR（#2 到 #11），每個主題單一、平均 20 分鐘從 commit 到 merge。

## 發現
原本以為「我有 5 件事要做、就開一個 PR 一次全做完最快」。實際反過來：

- **大 PR**：合併前要 review 100 行 diff，腦袋疲勞、漏看、卡住不敢合
- **小 PR**：30 行 diff，看 30 秒按 squash and merge，10 分鐘後 Vercel 上線

## 拆 PR 的判準
一個 PR 應該：
- 一個動詞 + 一個對象（feat: 加 X / chore: 升級 Y / fix: 修 Z）
- 合進去後**單獨能 deploy**，不依賴後續 PR
- diff 線數 < 200 行（資料/素材 PR 例外）

## 反案例
PR #9 原本應該是「security headers + canonical」純 chore，後來臨時加了「8 張知識封面」變成混合。雖然合得了，但 PR title 跟內容 diverge，未來查 git log 會困惑。

## 適用
所有有 CI/CD 的 git workflow。Vercel 預覽 + main 直推合作模式特別吃這套。
