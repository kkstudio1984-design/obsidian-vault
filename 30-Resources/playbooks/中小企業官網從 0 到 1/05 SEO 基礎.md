---
tags: [playbook, web, smb, seo]
chapter: 5
---

# 05 SEO 基礎｜技術 SEO 一次設好

## 必設 7 件事（30 分鐘）

| # | 項目 | 文件位置 |
| --- | --- | --- |
| 1 | sitemap.xml | `app/sitemap.ts` |
| 2 | robots.txt | `app/robots.ts` |
| 3 | metadata API（title / description / og） | `app/layout.tsx` + 各 page |
| 4 | canonical URLs | 各 page metadata |
| 5 | JSON-LD structured data | `lib/schema.ts` |
| 6 | Security headers | `next.config.js` |
| 7 | Google site verification meta | `app/layout.tsx` |

## 1. sitemap.xml（Next.js App Router）

```ts
// app/sitemap.ts
import type { MetadataRoute } from 'next';
import { getAllPublishedArticles } from '@/lib/notion';

const SITE = process.env.NEXT_PUBLIC_SITE_URL || 'https://example.com';

export default async function sitemap(): Promise<MetadataRoute.Sitemap> {
  const articles = await getAllPublishedArticles();
  return [
    { url: SITE, changeFrequency: 'daily', priority: 1.0 },
    { url: `${SITE}/services`, changeFrequency: 'weekly', priority: 0.9 },
    { url: `${SITE}/knowledge`, changeFrequency: 'weekly', priority: 0.9 },
    { url: `${SITE}/cases`, changeFrequency: 'weekly', priority: 0.8 },
    { url: `${SITE}/contact`, changeFrequency: 'monthly', priority: 0.7 },
    ...articles.map(a => ({
      url: `${SITE}/${routeOf(a.contentType)}/${a.slug}`,
      lastModified: a.lastEditedTime,
      changeFrequency: 'weekly' as const,
      priority: 0.8,
    })),
  ];
}
```

## 2. robots.txt

```ts
// app/robots.ts
export default function robots() {
  return {
    rules: { userAgent: '*', allow: '/' },
    sitemap: `${process.env.NEXT_PUBLIC_SITE_URL}/sitemap.xml`,
  };
}
```

## 3. metadata API

### Root layout（全站預設）

```ts
// app/layout.tsx
export const metadata: Metadata = {
  metadataBase: new URL(SITE),
  title: {
    default: '智廷工程行・金智消防｜...',
    template: '%s｜智廷工程行・金智消防',  // 子頁面自動套
  },
  description: '...',
  openGraph: { ... },
  robots: { index: true, follow: true },
  alternates: { canonical: SITE },
  verification: { google: 'xxx' },
};
```

### 各 index 頁（services/cases/knowledge/contact）

每頁要補 canonical + og url（不會從 layout 繼承）：

```ts
export const metadata: Metadata = {
  title: '服務項目',
  description: '...',
  alternates: { canonical: '/services' },
  openGraph: { url: '/services' },
};
```

### Dynamic 頁面（[slug]）

```ts
export async function generateMetadata({ params }): Promise<Metadata> {
  const a = await getArticleBySlug(params.slug);
  if (!a) return {};
  return {
    title: a.seoTitle || a.title,
    description: a.seoDescription,
    openGraph: {
      title: a.seoTitle || a.title,
      description: a.seoDescription,
      images: [a.coverImage],
      type: 'article',
      locale: 'zh_TW',
    },
    alternates: { canonical: `${SITE}/${routeType}/${a.slug}` },
  };
}
```

## 4. JSON-LD Schema（Google rich snippets）

### 首頁：LocalBusiness / HomeAndConstructionBusiness

```ts
export function businessSchema() {
  return {
    '@context': 'https://schema.org',
    '@type': 'HomeAndConstructionBusiness',  // 看行業選 type
    name: '智廷工程行（金智消防）',
    alternateName: '金智消防',
    legalName: '智廷工程行',
    foundingDate: '2023-03-16',
    telephone: '+886-925-369-737',
    taxID: '92528634',
    address: { '@type': 'PostalAddress', addressCountry: 'TW', addressRegion: '基隆市', ... },
    areaServed: [{ '@type': 'City', name: '基隆市' }, ...],
  };
}
```

### 文章頁：Article / TechArticle

```ts
export function articleSchema(article, routeType) {
  return {
    '@context': 'https://schema.org',
    '@type': routeType === 'cases' ? 'TechArticle' : 'Article',
    headline: article.title,
    description: article.seoDescription,
    image: article.coverImage,
    datePublished: article.publishDate,
    dateModified: article.lastEditedTime,
    author: { '@type': 'Person', name: '郭金智' },
    publisher: { '@type': 'Organization', name: '智廷工程行', alternateName: '金智消防' },
    mainEntityOfPage: { '@type': 'WebPage', '@id': `${SITE}/${routeType}/${article.slug}` },
  };
}
```

### 麵包屑：BreadcrumbList

```ts
export function breadcrumbSchema(items) {
  return {
    '@context': 'https://schema.org',
    '@type': 'BreadcrumbList',
    itemListElement: items.map((it, i) => ({
      '@type': 'ListItem',
      position: i + 1,
      name: it.name,
      item: it.url,
    })),
  };
}
```

### 注入頁面

```tsx
<script
  type="application/ld+json"
  dangerouslySetInnerHTML={{ __html: JSON.stringify(articleSchema(...)) }}
/>
```

驗證工具：https://validator.schema.org/

## 5. Security Headers

```js
// next.config.js
const securityHeaders = [
  { key: 'X-Frame-Options', value: 'SAMEORIGIN' },
  { key: 'X-Content-Type-Options', value: 'nosniff' },
  { key: 'Referrer-Policy', value: 'strict-origin-when-cross-origin' },
  { key: 'X-DNS-Prefetch-Control', value: 'on' },
  { key: 'Permissions-Policy', value: 'camera=(), microphone=(), geolocation=()' },
];

module.exports = {
  poweredByHeader: false,  // 關掉 X-Powered-By 指紋
  async headers() {
    return [{ source: '/:path*', headers: securityHeaders }];
  },
};
```

**CSP 暫不加** — 跟 GA / Meta Pixel / Notion 圖容易撞。等有資源做嚴格 CSP 再加。

## 6. Google Search Console

驗證 meta 注入：

```ts
// app/layout.tsx
verification: {
  google: '7Q9qNj99FBVLRaC9m89YxJLydPTrwdiUMlpgcPEUUvA',
},
```

驗證後在 GSC 提交 sitemap.xml。

## 7. ISR + on-demand revalidate

`/api/revalidate` route：

```ts
// 接 Notion 「🚀 立刻發布」button webhook
export async function POST(req: Request) {
  const secret = req.headers.get('x-revalidate-secret');
  if (secret !== process.env.REVALIDATE_SECRET) return 401;

  const { slug, type } = await req.json();
  const paths = ['/', `/${type}`, `/${type}/${slug}`];
  paths.forEach(p => revalidatePath(p));
  return { revalidated: true };
}
```

Notion 「🚀 button」設定 → 目標 URL `https://yoursite.com/api/revalidate` + header `x-revalidate-secret: <SECRET>` + body 含 slug。

## 預設 ISR 時間

| 路由 | revalidate | 為什麼 |
| --- | --- | --- |
| `/` | 預設 SSG | Hero 不常變 |
| `/services` | 3600（1h） | 索引頁，新文章上要快點看到 |
| `/cases` | 3600 | 同上 |
| `/knowledge` | 3600 | 同上 |
| `/services/[slug]` | 86400（24h） | 詳情頁變動少 |
| `/cases/[slug]` | 86400 | 同上 |
| `/knowledge/[slug]` | 86400 | 同上 |

> 都靠 webhook on-demand revalidate 即時更新，ISR 是保底。

下一章：[[06 CTA 系統]]
