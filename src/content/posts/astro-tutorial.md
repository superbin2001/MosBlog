---
title: 'Astro 使用指南'
description: '详细介绍 Astro 框架的基本用法和最佳实践。'
pubDate: '2024-01-20'
heroImage: 'https://images.unsplash.com/photo-1555066931-4365d14bab8c?w=800'
tags: ['Astro', '教程', '前端']
categories: ['教程']
---

# Astro 使用指南

Astro 是一个现代的静态站点生成器，非常适合构建内容驱动的网站。

## 项目结构

```
my-astro-blog/
├── src/
│   ├── content/
│   │   └── posts/
│   │       └── my-post.md
│   ├── layouts/
│   │   └── PostLayout.astro
│   └── pages/
│       └── index.astro
├── astro.config.mjs
└── package.json
```

## 内容集合

Astro 的内容集合（Content Collections）是管理 Markdown 内容的最佳方式。

### 定义集合

在 `src/content/config.ts` 中定义集合：

```typescript
import { defineCollection, z } from 'astro:content';

const posts = defineCollection({
  type: 'content',
  schema: z.object({
    title: z.string(),
    description: z.string(),
    pubDate: z.coerce.date(),
  }),
});

export const collections = { posts };
```

### 使用集合

在页面中获取内容：

```astro
---
import { getCollection } from 'astro:content';

const posts = await getCollection('posts');
---

<ul>
  {posts.map((post) => (
    <li>{post.data.title}</li>
  ))}
</ul>
```

## 布局组件

创建可复用的布局：

```astro
---
// src/layouts/BaseLayout.astro
const { title } = Astro.props;
---

<html>
  <head>
    <title>{title}</title>
  </head>
  <body>
    <slot />
  </body>
</html>
```

## 样式

Astro 支持多种样式方案：

- **原生 CSS**: 直接在 `.astro` 文件中写 `<style>`
- **Sass/SCSS**: 需要安装集成
- **Tailwind CSS**: 需要安装集成

## 部署

Astro 项目可以部署到任何静态托管服务：

- Vercel
- Netlify
- Cloudflare Pages
- GitHub Pages

只需运行 `npm run build`，然后将 `dist` 目录部署即可。

## 总结

Astro 为内容网站提供了一个简单、快速、灵活的解决方案。
