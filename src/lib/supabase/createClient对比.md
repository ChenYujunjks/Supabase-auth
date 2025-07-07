# 🧭 `createBrowserClient` vs `createServerClient` 全面对比

我会从使用场景、内部机制、状态存储方式、运行环境等多个维度来做一张对照图👇

---

## ✅ 一图对比

| 特性                   | `createBrowserClient`          | `createServerClient`               |
| -------------------- | ------------------------------ | ---------------------------------- |
| 📍 适用场景              | 浏览器端使用（前端组件）                   | 服务端使用（SSR、Edge Function、API Route） |
| ⚙️ 用途                | 自动管理 Auth 状态，给用户使用（登录/登出）      | 每次请求读取 Cookie，用于服务器判断身份            |
| 🧠 是否持久化登录状态         | ✅ 是（localStorage）              | ❌ 否（每次请求重新构建）                      |
| 🔁 是否自动刷新 token      | ✅ 是                            | ❌ 需要你自己实现（但通常不需要）                  |
| 🧠 是否监听 storage 事件   | ✅ 是（实现多 Tab 同步登录状态）            | ❌ 无 window，无法监听                    |
| 📦 默认存储方式            | `localStorage`                 | `cookies`（你传入）                     |
| 💻 是否能用于服务端渲染        | ❌ 不推荐，SSR 时会报错（无 window）       | ✅ 是（为 SSR/Edge Runtime 优化）         |
| 🧩 Supabase 自动登录方式   | ✅ 首次 magic link 登录时自动检测 URL 参数 | ✅ 可配合 cookies 自动识别                 |
| ⛔ 是否能访问 window / DOM | ✅ 可以                           | ❌ 不可以                              |
| 🔑 是否支持 RLS 安全访问     | ✅ 可支持（用户登录后 token 中带有用户 ID）    | ✅ 同样支持（从 cookie 拿 token）           |
| ⚠️ 是否依赖浏览器 API       | ✅ 强依赖（localStorage、window）     | ❌ 完全兼容 SSR/Edge                    |

---

## 📘 示例使用

### 📍 1. `createBrowserClient` 用在前端组件（必须加 `'use client'`）

```ts
// lib/supabase/client.ts
import { createBrowserClient } from '@supabase/ssr';

export function createClient() {
  return createBrowserClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
  );
}
```

使用：

```tsx
'use client';

import { createClient } from '@/lib/supabase/client';

const supabase = createClient();
const { data: user } = await supabase.auth.getUser(); // 前端自动带上 token
```

---

### 🌐 2. `createServerClient` 用在 `layout.tsx`, `page.tsx`, `middleware.ts`, `route.ts`

```ts
// lib/supabase/server.ts
import { cookies } from 'next/headers';
import { createServerClient } from '@supabase/ssr';

export function createClient() {
  return createServerClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!,
    { cookies }
  );
}
```

使用：

```ts
// app/protected/layout.tsx（在服务器渲染前判断身份）
const supabase = createClient();
const { data: { user } } = await supabase.auth.getUser();

if (!user) redirect('/auth/login');
```

---

## 🧠 核心记忆口诀：

| 用法场景                              | 用哪个函数                 |
| --------------------------------- | --------------------- |
| ✅ 前端组件                            | `createBrowserClient` |
| ✅ SSR 页面                          | `createServerClient`  |
| ✅ Edge API                        | `createServerClient`  |
| ✅ Layout 鉴权                       | `createServerClient`  |
| ❌ 在 SSR 中使用 `createBrowserClient` | 🚫 错误，会报错             |
| ❌ 在组件中使用 `createServerClient`     | 🚫 错误，cookies 不可用     |

---

## 🎯 小结

> Supabase SDK 是根据**运行环境**选择不同的创建方式的。你只需要记住一句话：

> ✅「前端组件用 `createBrowserClient`，服务器端用 `createServerClient`」，并记得传入 `.env` 变量和上下文（cookies）。
