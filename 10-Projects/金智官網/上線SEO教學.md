# 金智官網｜上線 SEO 完整教學

> 給你 / 自己跟著做的 step-by-step 操作指南。  
> 目標：讓 Google 找到網站、開始抓內容、慢慢累積搜尋流量。  
> 預估時間：A+B 約 30 分鐘，C 看你要不要做。

---

## 為什麼現在 Google 找不到

技術 SEO（sitemap、robots、canonical、structured data）已經全部到位，但：

1. **沒提交給 Google Search Console** ← 主因，Google 不知道有這站
2. **網域是 vercel.app 子網域**，不是 kingzhi.com — SEO 略不利

修這兩個就會慢慢有收錄。

---

## A. 提交 Google Search Console（5 分鐘）

### 步驟

1. 開 https://search.google.com/search-console
2. 用 **kkstudio1984@gmail.com** 登入（或郭老闆的 Google 帳號，看誰負責 SEO）
3. 左上「新增資源」→ 選 **「URL 前置字元」**（不要選網域）
4. 貼 `https://kingzhi-web.vercel.app` → 繼續
5. 驗證方式：選 **「HTML 標籤」**
6. 複製類似這樣的 meta 標籤：
   ```html
   <meta name="google-site-verification" content="abc123xxxx_..." />
   ```
7. **把整個 content="xxx" 那串貼給我**，我幫你加到 `app/layout.tsx`
8. 我 commit + push 後合 PR、Vercel 重 build（約 40 秒）
9. 回 Search Console 按 **「驗證」** 按鈕
10. 看到「已驗證擁有權」綠勾即成功

### 提交 Sitemap

驗證完成後：

1. 左側選單 → **「Sitemaps」**
2. 「新增 Sitemap」→ 輸入 `sitemap.xml`
3. 提交
4. 等狀態變「成功」（通常 5–60 分鐘）

### 接下來

- 1–7 天內 Google 開始爬
- 1–4 週內有第一筆排名
- Search Console 會慢慢顯示「成效」「索引」資料

---

## B. 接上 kingzhi.com 網域（強烈建議）

需要：**域名持有權（DNS 控制權）**。  
通常是郭老闆或當初註冊的人。

### B-1. 先確認誰持有

1. 開 https://whois.com/whois/kingzhi.com
2. 看「Registrar」（HiNet / GoDaddy / Namecheap / 戰國策...）
3. 持有人應該登得進那家公司的後台

### B-2. 在 Vercel 加 Domain

1. 開 https://vercel.com/kkstudio1984-designs-projects/kingzhi-web/settings/domains
2. 「Add Domain」→ 輸入 `kingzhi.com`
3. 同時加 `www.kingzhi.com`
4. Vercel 會顯示要設定的 DNS records，**截圖記下來**，看起來像：

   ```
   Type   Name   Value
   A      @      76.76.21.21
   CNAME  www    cname.vercel-dns.com.
   ```

### B-3. 到 DNS 後台改

1. 登入 DNS 後台（HiNet 是「我的網域」、Namecheap 是「Advanced DNS」）
2. **刪除既有的 A / CNAME / AAAA records**（如果有指其他地方）
3. 依 Vercel 提供的設定加新的 records
4. TTL（存活時間）選 **3600 秒**或 **預設**
5. 儲存

### B-4. 等 DNS 生效

- 通常 **15 分鐘到 24 小時**
- 在 https://www.whatsmydns.net/#A/kingzhi.com 看全球 DNS 是否生效
- Vercel 後台 Domains 頁會自動偵測，綠勾出現代表 OK

### B-5. 改 `NEXT_PUBLIC_SITE_URL`

DNS 接通後：

1. Vercel 後台 → Settings → Environment Variables
2. 找 `NEXT_PUBLIC_SITE_URL`
3. 改成 `https://kingzhi.com`
4. 重新部署（最新 deployment 旁的 `⋯` → Redeploy）

### B-6. 把 Search Console 也加新網域

回 Search Console，**用「URL 前置字元」再加 `https://kingzhi.com`**，重新驗證 + 提交 sitemap。

> 舊網域（vercel.app）的索引會慢慢移轉。建議在 `next.config.js` 加一條重新導向：
> ```js
> async redirects() {
>   return [
>     { source: '/:path*', has: [{ type: 'host', value: 'kingzhi-web.vercel.app' }],
>       destination: 'https://kingzhi.com/:path*', permanent: true },
>   ];
> },
> ```
> 不過這要 kingzhi.com 接通後再加，不然會自己擋自己。

---

## C. Google 商家檔案（B2B 必做，但要實體店）

消防工程業者，**Google 商家檔案 = 北北基地區 SEO 的核武**。  
郭老闆未來在「基隆消防」「附近消防工程」搜尋詞被找到的關鍵。

### C-1. 申請

1. 開 https://business.google.com
2. 用同一個 Google 帳號登入
3. 「新增商家」→ 填：
   - 商家名稱：**智廷工程行**（不要寫金智消防，依登記名稱）
   - 類別：**消防安全設備服務 / Fire protection service**
   - 地點：選「**是的**」（有實體營業地點）
   - 地址：基隆市安樂區基金一路 135 巷 40 號 3 樓
4. 服務地區：**勾「我也提供服務地區的客戶」**，選北北基三縣市
5. 電話：0925-369-737
6. 網站：`https://kingzhi-web.vercel.app`（之後改 kingzhi.com）

### C-2. 驗證

Google 會寄一張**明信片**到你登記的地址（基隆基金一路），上面有驗證碼。
- 大概 **3–14 天**會到
- 收到後回 business.google.com 輸入驗證碼

### C-3. 隱私考量

⚠️ 之前 SPEC 決定**不放 Google Map**因為地址是 3 樓住家。但 Google 商家檔案 **必須有實體地址驗證**。

兩種折衷：

| 做法 | 隱私 | SEO |
| --- | --- | --- |
| 不申請商家檔案 | 完全隱蔽 | 失去地區 SEO 大資產 |
| 申請但**只勾「服務地區」、不顯示精確地址** | 公網看不到地址但商家檔案存在 | SEO 命中、隱私保留 |
| 申請且顯示完整地址 | 地址公開 | SEO 命中最強 |

**建議走中間：** 申請時在「您是否要在 Google 上顯示這個地址？」選 **「不顯示」**，僅勾「服務地區」。地址只有 Google 內部知道（用於驗證身分），公網不會出現。

### C-4. 申請後優化

商家檔案開通後每週做：

- 加照片（工程現場、員工合照、辦公室）
- 回覆評論
- 發**Google 貼文**（限時優惠、節氣提醒、最新案例）

---

## 預期時程

| 動作 | 開始有效果 | 看得到搜尋流量 |
| --- | --- | --- |
| A. Search Console 提交 | 1–7 天 | 4 週後 |
| B. kingzhi.com 接上 | 1 天 | 同上（+ 4 週重收錄） |
| C. Google 商家檔案 | 14 天（驗證後）| 立即顯示在地圖 / 商家搜尋 |

---

## 你現在最該做的順序

1. **A** 立刻做 — 5 分鐘成本最低、效益最早出來
2. **B** 找郭老闆問域名持有狀況，週末安排
3. **C** 同步申請，因為要等明信片 14 天，越早起跑越好

任何步驟卡住把畫面截給我，我幫你 debug。
