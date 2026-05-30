---
tags: [playbook, web, smb, cheatsheet]
---

# Cheat Sheet｜中小企業官網一頁速查

## 開工前必問

```
□ 公司全名 + 統編 + 設立日 + 地址 + 負責人
□ 主品牌 vs SEO 品牌順序
□ 1-2 個主要客群（不超過 2 個）
□ 對外電話 / Email / LINE 各 1 個
□ 不能寫的：隱私 / 競品 / 客戶名
□ 第一批內容：服務頁幾個、案例幾個、文章幾個
```

## 技術棧

```
Next.js 14 App Router + Tailwind
Notion CMS（headless）
Vercel Hobby
GitHub private + gh CLI
GA4 + Meta Pixel + Resend + LINE Messaging API
```

## Notion DB schema

```
一個 DB 管全部
contentType: 📝 部落格 | 🔧 案例 | 🛠 服務頁
必要欄位: 標題 / Slug / 客群 / 關鍵字類別 / SEO Title / SEO Desc / 封面圖 / 作者 / 上稿日 / 字數 / 狀態 / Tags / 支柱關聯
狀態用 select 不是 status
```

## fallback chain

```ts
coverImage = notionCover  // 1. Notion 上傳的
  ?? slugFallback         // 2. /images/<type>/<slug>.png
  ?? '/images/og-default.jpg'  // 3. 統一退路
```

## AI 圖三層構圖

```
前景 hero（1 主物件）
+ 中景敘事道具（3–5 個）
+ 背景虛化環境
+ 暖金+冷藍對比光線
+ mid-action 動感
+ negative: no people, no text, no logos
+ --ar 1.91:1
```

## SEO 7 件

```
1. sitemap.xml      (app/sitemap.ts)
2. robots.txt       (app/robots.ts)
3. metadata + canonical (各 page)
4. JSON-LD          (lib/schema.ts)
5. Security headers (next.config.js)
6. GSC verification (layout.tsx)
7. ISR + webhook    (/api/revalidate)
```

## CTA 三鼎立

```
📞 電話 tel:0925369737
💬 LINE https://lin.ee/xxx (target=_blank)
📝 表單 modal (event-driven)
```

全部從 `lib/contact.ts` 單一 source

## Git workflow

```
git fetch origin
git checkout -b feat/xxx origin/main
# 做事
git add specific-files
git commit -m "..."
git push -u origin feat/xxx
gh pr create ...
# squash and merge
```

## 上線 checklist

```
□ Search Console 驗證 + 提交 sitemap
□ Google 商家檔案申請（明信片 14 天）
□ 接正式網域 + 改 NEXT_PUBLIC_SITE_URL
□ Resend 域名驗證 SPF/DKIM
□ Lighthouse ≥ 90 × 4 項
□ Mobile 跨裝置測
```

## 內容比例（最少版）

```
4 個 cluster × 1 支柱文 = 4 篇知識文章
6 個服務頁
3 個代表案例（最少）
1 個首頁
1 個聯絡頁
= 15 頁 SEO 可索引內容
```

## 預估時間

```
規劃 + SPEC      : 1 hr
技術設定          : 1 hr
首頁 + 元件      : 4 hr
內容 page type 結構: 2 hr
6 服務頁         : 2 hr
3 案例           : 1 hr
4 知識文章         : 4 hr
SEO + 部署       : 2 hr
總計            : 17 hr
```

熟練 1 天衝刺 + 內容慢慢補。
