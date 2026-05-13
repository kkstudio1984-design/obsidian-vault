---
tags: [playbook, web, smb, conversion]
chapter: 6
---

# 06 CTA 系統｜電話 + LINE + 表單三鼎立

## 設計原則

**三類 CTA 並陳，覆蓋三種顧客心理：**

| 顧客類型 | 偏好 CTA | 期望速度 |
| --- | --- | --- |
| 急件處理（被罰單、設備壞） | 📞 電話 | 立刻 |
| 想先傳照片問問看（怕浪費對方時間） | 💬 LINE | 半天內 |
| 想正式留資料（管委會、企業詢價） | 📝 表單 | 1–2 天內 |

**少了任一類就掉一群客戶。**

## 中央 constants 管理

`lib/contact.ts` 集中所有對外聯絡資料：

```ts
export const PHONE = '0925369737';
export const PHONE_DISPLAY = '0925-369-737';

export const LINE_URL = 'https://lin.ee/uwtymRR';  // 換號只動這一處

const OPEN_EVENT = 'kingzhi:open-contact-modal';

export function openContactModal() {
  if (typeof window === 'undefined') return;
  window.dispatchEvent(new Event(OPEN_EVENT));
}

export const CONTACT_MODAL_EVENT = OPEN_EVENT;
```

換 LINE / 電話只改一處，全站自動跟上。

## CTA 出現的 7 個位置

| 位置 | 內容 | 元件 |
| --- | --- | --- |
| Navbar 右側 | 📞（桌機顯示電話） | `Navbar.tsx` |
| Hero 區下方 | 📞 + 💬 + 📝 | `Hero.tsx` |
| 文章詳情側邊 | 📞 + 💬 + 📝（黏著） | `StickyCTA.tsx` |
| 文章詳情底部 | 📞 + 💬 + 📝（大塊） | `BottomCTA.tsx` |
| 浮動按鈕（桌機右下） | 📞 + 💬 + 📝 | `FAB.tsx` |
| 手機底部黏條 | 📞 + 💬 + 📝 | `MobileBottomBar.tsx` |
| 聯絡頁 | 完整表單 + QR + 電話 | `app/contact/page.tsx` |

## 表單 modal 設計（事件驅動）

避免 prop drilling 與 Context boilerplate，用 custom event：

```tsx
// components/ContactModal.tsx
'use client';
import { useEffect, useState } from 'react';
import { ContactForm } from './ContactForm';
import { CONTACT_MODAL_EVENT } from '@/lib/contact';

export function ContactModal() {
  const [open, setOpen] = useState(false);

  useEffect(() => {
    const handler = () => setOpen(true);
    window.addEventListener(CONTACT_MODAL_EVENT, handler);
    return () => window.removeEventListener(CONTACT_MODAL_EVENT, handler);
  }, []);

  // 鎖背景捲動
  useEffect(() => {
    if (!open) return;
    document.body.style.overflow = 'hidden';
    return () => { document.body.style.overflow = ''; };
  }, [open]);

  // ESC 關閉
  useEffect(() => {
    if (!open) return;
    const onKey = (e: KeyboardEvent) => e.key === 'Escape' && setOpen(false);
    window.addEventListener('keydown', onKey);
    return () => window.removeEventListener('keydown', onKey);
  }, [open]);

  if (!open) return null;
  return (
    <div role="dialog" onClick={() => setOpen(false)} className="modal-backdrop">
      <div onClick={(e) => e.stopPropagation()} className="modal-content">
        <button onClick={() => setOpen(false)}>×</button>
        <ContactForm />
      </div>
    </div>
  );
}
```

**掛 layout.tsx 一次，全站任一個 button 觸發**。

## 表單後端（/api/contact）

```ts
const Body = z.object({
  name: z.string().min(1).max(50),
  phone: z.string().regex(/^09\d{2}-?\d{3}-?\d{3}$/),
  email: z.string().email().optional().or(z.literal('')),
  message: z.string().min(1).max(1000),
  targetAudience: z.enum(['🟢 業主／店家', '🏠 社區管委會／主委']),
  sourcePage: z.string(),
  honeypot: z.string().optional(),  // 機器人陷阱
});

export async function POST(req: Request) {
  const body = Body.parse(await req.json());
  if (body.honeypot) return { ok: true };  // 機器人靜默 fake 成功

  const notifyText = `🔥 新詢問\n姓名：${body.name}\n...`;

  await Promise.allSettled([
    sendResend(body, notifyText),   // 寄 email
    sendLineMessaging(notifyText),   // 推 LINE 群組
  ]);

  return { ok: true };
}
```

## 表單三重防護

1. **honeypot**：肉眼看不到的 input（`tabIndex={-1}`, `position: absolute, left: -9999px`），機器人填了 → 靜默假成功
2. **Zod 驗證**：手機格式、字數上限、enum
3. **Rate limit**（未上線時可不做，量大再加 Upstash KV）

## LINE Messaging API（不是 LINE Notify）

LINE Notify 已停服。改用 Messaging API：

```ts
async function sendLineMessaging(text) {
  await fetch('https://api.line.me/v2/bot/message/push', {
    method: 'POST',
    headers: {
      Authorization: `Bearer ${process.env.LINE_CHANNEL_ACCESS_TOKEN}`,
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      to: process.env.LINE_TARGET_GROUP_ID,
      messages: [{ type: 'text', text }],
    }),
  });
}
```

設定步驟：
1. 申請 LINE Bot Channel
2. 加 bot 到通知群組
3. 取得 channel access token + group ID
4. 設環境變數

## 埋點（analytics）

每次 CTA 點擊都要 track：

```ts
// lib/analytics.ts
export function trackPhoneClick(source: string) {
  if (typeof window === 'undefined') return;
  window.gtag?.('event', 'phone_click', { source });
  window.fbq?.('trackCustom', 'PhoneClick', { source });
}

export function trackLineClick(source: string) { ... }
export function trackContactSubmit(audience: string) { ... }
```

`source` 標 hero / sticky / bottom / fab / mobile-bottom / navbar — 知道哪個位置最強。

下一章：[[07 部署上線]]
