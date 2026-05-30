# 金智官網｜AI 圖片提示詞

> 用途：產 Hero / og / 作者頭像 / 30 篇文章封面的 AI 圖。  
> 風格基準：黑金 luxury（站上 CSS `#0f0f0f` 黑底 + `#c9a876` 金）。  
> 工具不挑：Midjourney / Adobe Firefly / DALL-E 3 都可。下方 prompt 已照 MJ 語法寫（`--ar`, `--style raw`），其他工具去掉那兩個參數即可。

---

## 1. Hero 背景（1920×900）

挑一個方向產。

### 方向 A：配管／檢修工地特寫（最寫實，建議）

```
Cinematic close-up of industrial fire safety piping and red sprinkler heads
mounted on a polished black ceiling, soft golden rim lighting, shallow depth
of field, professional documentary photography, dark moody atmosphere with
warm gold accents, ultra-realistic, 35mm lens, --ar 16:9 --style raw
Negative: cartoon, illustration, people, faces, text, watermark, low quality
```

### 方向 B：消防栓／警報器抽象線稿（最 luxury）

```
Minimal abstract line art of a fire hydrant and smoke detector silhouette,
luxurious matte black background with thin warm gold outlines and subtle
particle glow, premium editorial style, art deco influence, geometric and
elegant, ultra clean, --ar 16:9 --style raw
Negative: photo realism, cartoon, busy details, people, text, watermark
```

### 方向 C：夜景商辦廠房外觀（B2B 信任感）

```
Wide angle low-light photograph of a Taiwanese mid-rise commercial building
exterior at dusk, warm amber emergency lighting visible through windows,
polished black glass facade, faint gold hour-of-blue sky, professional
architectural photography, calm and authoritative mood, --ar 16:9 --style raw
Negative: people, cartoon, signage, brand logos, watermark, low quality
```

存檔位置：`public/images/hero.jpg`

---

## 2. og-default.jpg（1200×630）社群分享預設圖

```
Premium dark-mode social card background, deep matte black gradient
(#0f0f0f to #1a1a1a) with soft gold particle bokeh in lower-right,
faint geometric accent lines in warm gold (#c9a876), centered vertical
breathing space for overlay text, luxurious B2B service brand aesthetic,
no text in image (text will be added later), --ar 1.91:1 --style raw
Negative: text, logo, people, cartoon, busy details, watermark
```

產完用 Figma / Canva 套字：「智廷工程行・金智消防｜20+ 年消防工程實戰」

存檔位置：`public/og-default.jpg`

---

## 3. 作者頭像（144×144 圓形）

不用真實人臉，兩條路擇一：

### A. 抽象工頭剪影（無臉）

```
Side silhouette of a mature male in a dark navy work uniform with safety
helmet, three-quarter back view, no facial features visible, deep matte
black background with subtle warm gold rim light, professional editorial
portrait, square framing, --ar 1:1 --style raw
Negative: face, eyes, mouth, cartoon, illustration, text, watermark
```

### B. Monogram 字標代替

```
Elegant monogram "郭" or "JZ" in serif typography, embossed in warm
gold (#c9a876) on a deep matte black circular background, subtle bevel
and soft glow, premium personal brand mark, --ar 1:1 --style raw
Negative: photo, realistic, people, faces, busy patterns
```

存檔位置：`public/images/author.jpg`

---

## 4. 文章封面範本（1200×630）批量用

把 `{TITLE}` 與 `{KEYWORD_CLASS_HINT}` 換成每篇實際內容：

```
Editorial-style header image for a Taiwanese fire safety industry blog
article titled "{TITLE}". Theme hint: {KEYWORD_CLASS_HINT}. Composition:
abstract minimalist scene with one focal fire-safety object (no people,
no text), shallow depth, deep matte black backdrop (#0f0f0f), warm gold
(#c9a876) accent lighting from upper-left, premium B2B documentary
photography aesthetic, --ar 1.91:1 --style raw
Negative: text, watermark, cartoon, people, faces, low quality
```

`{KEYWORD_CLASS_HINT}` 對照表：

| 關鍵字類別 | hint 用詞 |
| --- | --- |
| 🔴 商業搜尋詞 | commercial fire alarm panel and inspection clipboard on a desk |
| 🟡 痛點／流程詞 | bureaucratic paperwork stack with a fire safety stamp and red ribbon |
| 🟠 檢修申報詞 | mechanical fire valve and pressure gauge being checked with a tool |
| 🔵 地區詞 | aerial silhouette of Taipei or Keelung skyline at dusk with one warm-lit building |

存檔位置：上傳到 Notion 文章「封面圖」欄位（build 時自動下載到 `public/images/notion/`）

---

## 5. 工具與授權建議

| 工具 | 風格特點 | 商用授權 |
| --- | --- | --- |
| Midjourney v6/v7 | 紀錄片質感、最有風格 | Pro 方案以上才商用 |
| Adobe Firefly | 乾淨設計感、賠付保證 | 商用最乾淨 |
| DALL-E 3（ChatGPT） | 中英文 prompt 都可 | ChatGPT Plus 即可商用 |
| Flux.1 Pro | 寫實偏 photographic | 看部署平台條款 |

> 30 篇文章封面建議走 Adobe Firefly 或 DALL-E 3 — 商用授權最簡單，量產壓力低。

---

## 6. 產完後存檔規則

| 檔名 | 位置 |
| --- | --- |
| hero.jpg | `D:\GOLD\kingzhi-web\public\images\hero.jpg` |
| author.jpg | `D:\GOLD\kingzhi-web\public\images\author.jpg` |
| og-default.jpg | `D:\GOLD\kingzhi-web\public\og-default.jpg` |
| 文章封面 | 直接傳 Notion DB 的「封面圖」欄位，build 時自動下載 |

> Next.js 會自動把 jpg/png 轉 webp/avif 給瀏覽器，不需手動轉檔。  
> 圖片放好 push main → Vercel 自動部署 ~40s 後上線。
