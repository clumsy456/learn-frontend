# Day 18：CSS 工具与组件库 + 第三周项目

#### 学习内容

**1. Tailwind CSS（原子化 CSS — 推荐！）**

```jsx
// 安装
// pnpm add -D tailwindcss postcss autoprefixer
// npx tailwindcss init -p

// 使用 — 直接在 className 中写样式
function Card({ title, description, image }) {
  return (
    <div className="max-w-sm rounded-lg shadow-md overflow-hidden bg-white hover:shadow-xl transition-shadow duration-300">
      <img src={image} alt={title} className="w-full h-48 object-cover" />
      <div className="p-6">
        <h3 className="text-xl font-bold text-gray-900">{title}</h3>
        <p className="mt-2 text-gray-600">{description}</p>
        <button className="mt-4 px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600 transition-colors">
          了解更多
        </button>
      </div>
    </div>
  );
}

// 后端工程师视角：
// Tailwind 的好处：
// 1. 不需要在 CSS 文件和 HTML 之间跳来跳去
// 2. 约束了设计系统（颜色、间距、字体大小都是预定义的）
// 3. 删除组件时，样式也一起删除（没有 CSS 垃圾堆积）
// 4. 类名即文档（看到 className 就知道样式）
```

**2. 常用 UI 组件库**

| 库 | 特点 | 适用场景 |
|----|------|----------|
| **shadcn/ui** | 可复制粘贴的组件，基于 Radix UI + Tailwind | React + Tailwind 项目（推荐） |
| **Ant Design** | 企业级组件库，功能全面 | 中后台管理系统 |
| **Material UI** | Google Material Design 风格 | 需要 Material 风格的项目 |
| **Headless UI** | 无样式组件，完全自定义 | 需要独特设计 |
| **Radix UI** | 无障碍优先的无头组件 | 构建自己的组件库 |

```bash
# shadcn/ui（推荐）
pnpm dlx shadcn@latest init
pnpm dlx shadcn@latest add button dialog dropdown-menu

# Ant Design
pnpm add antd
```

**3. CSS-in-JS（了解即可）**

```jsx
// styled-components（较少用了，但了解一下）
import styled from 'styled-components';

const Button = styled.button`
  background: ${props => props.primary ? '#3b82f6' : '#6b7280'};
  color: white;
  padding: 8px 16px;
  border-radius: 4px;
  &:hover {
    opacity: 0.9;
  }
`;
```

#### 第三周项目：全功能博客前端

**需求**：
- 首页（文章列表 + 分页 + 搜索）
- 文章详情页（Markdown 渲染 + 代码高亮）
- 分类/标签页
- 关于页面
- 暗色模式
- 响应式设计
- SEO 优化（meta tags）
- 加载状态和错误处理

**技术栈**：
- React + TypeScript + Vite
- React Router
- Zustand 状态管理
- Tailwind CSS + shadcn/ui
- 模拟 API（json-server 或 MSW）
