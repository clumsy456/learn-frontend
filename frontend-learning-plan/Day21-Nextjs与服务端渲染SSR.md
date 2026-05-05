# Day 21：Next.js 与服务端渲染（SSR）

#### 学习内容

```
渲染模式对比（后端工程师必懂！）：

CSR（Client-Side Rendering）— 传统 SPA
  浏览器下载空 HTML → 下载 JS → 执行 JS → 渲染页面
  优点：交互流畅、服务器压力小
  缺点：首屏慢、SEO 差
  类比：Go 返回空页面，前端 JS 填充内容

SSR（Server-Side Rendering）— Next.js 默认
  服务器执行 JS → 生成完整 HTML → 返回给浏览器
  优点：首屏快、SEO 好
  缺点：服务器压力大、TTFB 增加
  类比：Go 的 html/template 渲染

SSG（Static Site Generation）— 构建时生成
  构建时生成所有页面的 HTML → CDN 分发
  优点：最快、最便宜
  缺点：内容不实时
  类比：Go 生成静态 HTML 文件

ISR（Incremental Static Regeneration）— 增量静态再生
  SSG + 定期重新生成
  类比：Go 的缓存 + TTL
```

```bash
# 创建 Next.js 项目
pnpm create next-app my-blog --typescript --tailwind --app
```

```tsx
// app/page.tsx — 服务端组件（默认）
// 这是服务端渲染的！不会发送到浏览器
async function HomePage() {
  // 可以直接访问数据库
  const posts = await db.post.findMany();
  
  return (
    <div>
      <h1>博客文章</h1>
      {posts.map(post => (
        <article key={post.id}>
          <h2>{post.title}</h2>
          <p>{post.excerpt}</p>
        </article>
      ))}
    </div>
  );
}

// 客户端组件（需要交互时）
'use client';
import { useState } from 'react';

function SearchBar() {
  const [query, setQuery] = useState('');
  // 这个组件会在浏览器中执行
  return <input value={query} onChange={e => setQuery(e.target.value)} />;
}

// API 路由（后端工程师最熟悉的部分！）
// app/api/hello/route.ts
import { NextResponse } from 'next/server';

export async function GET(request: Request) {
  // 这就是一个标准的 Web API handler！
  const { searchParams } = new URL(request.url);
  const name = searchParams.get('name') || 'World';
  
  return NextResponse.json({ message: `Hello, ${name}!` });
}

export async function POST(request: Request) {
  const body = await request.json();
  // 处理 POST 请求...
  return NextResponse.json({ success: true });
}

// 后端类比：
// Next.js API Routes ≈ Go 的 http.HandlerFunc
// 服务端组件 ≈ Go 的模板渲染
// 客户端组件 ≈ Go 返回的 JS，浏览器执行
```
