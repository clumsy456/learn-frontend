# 🚀 资深后端工程师 → 前端全栈：一个月超级详细学习计划

> **适用人群**：精通 Golang/Python 的资深后端工程师，有扎实编程基础，希望系统掌握前端全栈知识
> **学习周期**：4 周（每周 6 天，每天 4-6 小时，可根据实际情况调整）
> **学习理念**：利用后端经验快速类比迁移，重点攻克前端特有概念，以项目驱动学习

---

## 📋 目录

- [前置准备](#前置准备)
- [第一周：HTML/CSS 基础与页面构建](#第一周htmlcss-基础与页面构建)
- [第二周：JavaScript 深度精讲](#第二周javascript-深度精讲)
- [第三周：现代前端框架与工程化](#第三周现代前端框架与工程化)
- [第四周：进阶实战与全栈打通](#第四周进阶实战与全栈打通)
- [附录：学习资源汇总](#附录学习资源汇总)

---

## 前置准备

### 工具安装（第 0 天）

| 工具 | 用途 | 安装方式 |
|------|------|----------|
| **VS Code** | 主力编辑器 | 官网下载或 `brew install --cask visual-studio-code` |
| **Node.js (LTS)** | JavaScript 运行时 | `nvm install --lts` 或官网下载 |
| **pnpm** | 包管理器（比 npm 更快） | `npm install -g pnpm` |
| **Chrome DevTools** | 调试利器 | Chrome 浏览器自带（F12） |
| **Git** | 版本控制 | 你应该已经有了 |
| **浏览器扩展** | Vue/React DevTools | Chrome Web Store 搜索安装 |

### VS Code 必装插件

- **ESLint** — 代码规范检查
- **Prettier** — 代码格式化
- **Tailwind CSS IntelliSense** — Tailwind 智能提示
- **Auto Rename Tag** — 自动重命名 HTML 标签
- **Path Intellisense** — 路径自动补全
- **GitLens** — Git 增强

### 心态调整（后端工程师必读）

```
后端思维 → 前端思维的转换：

1. "一次编写，到处运行" → "一次编写，到处不兼容"（浏览器差异）
2. "编译时就能发现错误" → "运行时才知道炸了"（动态类型 + 弱类型）
3. "服务端渲染一切" → "客户端渲染 + 服务端渲染 + 静态生成"（多种渲染模式）
4. "状态在数据库里" → "状态散落在组件、URL、Cookie、LocalStorage 中"
5. "API 返回 JSON" → "你需要把 JSON 变成用户看到的 UI"
6. "并发用 goroutine" → "并发用 Promise/async-await/事件循环"
7. "测试用单元测试" → "测试用单元测试 + E2E 测试 + 组件测试"
```

---

## 第一周：HTML/CSS 基础与页面构建

> **本周目标**：掌握 HTML5 语义化标签、CSS3 核心特性、Flex/Grid 布局、响应式设计，能独立还原设计稿
> **后端类比**：HTML ≈ 数据结构定义，CSS ≈ 数据展示层，浏览器 ≈ 渲染引擎

---

### Day 1：HTML5 语义化与文档结构

#### 学习内容

**1. HTML 文档基本结构**
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="页面描述（SEO 重要）">
  <title>页面标题</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <!-- 页面内容 -->
  <script src="app.js" defer></script>
</body>
</html>
```

**2. 语义化标签（重点！）**

| 标签 | 用途 | 后端类比 |
|------|------|----------|
| `<header>` | 页头/区块头部 | — |
| `<nav>` | 导航栏 | 路由表 |
| `<main>` | 主内容区 | Controller 的主逻辑 |
| `<article>` | 独立内容块 | 一条完整的数据记录 |
| `<section>` | 主题性分组 | 功能模块划分 |
| `<aside>` | 侧边栏/附加信息 | 补充数据 |
| `<footer>` | 页脚 | — |
| `<figure>` / `<figcaption>` | 图片+说明 | 数据+元数据 |
| `<time>` | 时间标记 | 时间戳格式化 |
| `<details>` / `<summary>` | 可折叠内容 | 手风琴组件 |

**3. 表单与输入（后端常打交道）**
```html
<form action="/api/login" method="POST">
  <!-- 文本输入 -->
  <input type="text" name="username" placeholder="用户名" required>
  
  <!-- 邮箱（自带格式验证） -->
  <input type="email" name="email">
  
  <!-- 密码 -->
  <input type="password" name="password" minlength="8">
  
  <!-- 数字 -->
  <input type="number" name="age" min="0" max="150">
  
  <!-- 日期 -->
  <input type="date" name="birthday">
  
  <!-- 文件上传 -->
  <input type="file" name="avatar" accept="image/*">
  
  <!-- 下拉选择 -->
  <select name="role">
    <option value="admin">管理员</option>
    <option value="user">普通用户</option>
  </select>
  
  <!-- 多行文本 -->
  <textarea name="bio" rows="4"></textarea>
  
  <!-- 单选 -->
  <input type="radio" name="gender" value="male"> 男
  <input type="radio" name="gender" value="female"> 女
  
  <!-- 复选 -->
  <input type="checkbox" name="hobbies" value="coding"> 编程
  
  <!-- 隐藏字段 -->
  <input type="hidden" name="csrf_token" value="xxx">
  
  <!-- 提交 -->
  <button type="submit">登录</button>
</form>
```

**4. 多媒体标签**
```html
<!-- 图片（响应式） -->
<img src="photo.jpg" alt="描述" loading="lazy" 
     srcset="photo-320w.jpg 320w, photo-640w.jpg 640w"
     sizes="(max-width: 600px) 320px, 640px">

<!-- 视频 -->
<video controls width="640">
  <source src="video.mp4" type="video/mp4">
  <source src="video.webm" type="video/webm">
</video>

<!-- 音频 -->
<audio controls>
  <source src="audio.mp3" type="audio/mpeg">
</audio>
```

**5. SEO 与无障碍（Accessibility / a11y）**
```html
<!-- ARIA 属性：让屏幕阅读器理解 -->
<button aria-label="关闭菜单" aria-expanded="false">
  <span aria-hidden="true">&times;</span>
</button>

<!-- 图片必须有 alt -->
<img src="chart.png" alt="2024年Q1销售额柱状图">

<!-- 语义化的 heading 层级 -->
<h1>页面主标题（每页只有一个）</h1>
  <h2>一级章节</h2>
    <h3>二级章节</h3>
  <h2>另一个一级章节</h2>
```

#### 实战练习

1. **用纯 HTML 写一个博客文章页面**，包含：header（logo + nav）、文章主体（标题、作者、时间、正文、图片、代码块）、侧边栏（目录、相关文章）、footer
2. **写一个注册表单**，覆盖所有 input 类型，注意 label 关联（`<label for="id">`）

#### 今日关键概念

- `<!DOCTYPE html>` 告诉浏览器用标准模式渲染（不是怪异模式）
- `<script defer>` vs `<script async>` vs `<script>` 的区别（类比 Go 的 goroutine 调度）
  - **无属性**：阻塞 HTML 解析，下载完立即执行
  - **defer**：不阻塞解析，HTML 解析完后按顺序执行（推荐）
  - **async**：不阻塞解析，下载完立即执行，不保证顺序
- `<meta viewport>` 是移动端适配的关键

---

### Day 2：CSS 选择器与盒模型

#### 学习内容

**1. CSS 引入方式（优先级从低到高）**
```css
/* 1. 外部样式表（推荐） */
<link rel="stylesheet" href="style.css">

/* 2. 内部样式表 */
<style>
  p { color: red; }
</style>

/* 3. 行内样式（尽量避免） */
<p style="color: red;">文本</p>
```

**2. 选择器大全（从宽到窄）**

```css
/* === 基础选择器 === */
* { }                    /* 通配符选择器 — 性能差，少用 */
p { }                    /* 元素选择器 */
.class-name { }          /* 类选择器 — 最常用 */
#id-name { }             /* ID 选择器 — 唯一，少用 */

/* === 组合选择器 === */
div p { }                /* 后代选择器 — div 下所有 p */
div > p { }              /* 子选择器 — div 的直接子 p */
div + p { }              /* 相邻兄弟选择器 — div 后面紧跟的 p */
div ~ p { }              /* 通用兄弟选择器 — div 后面所有 p */

/* === 属性选择器 === */
input[type="text"] { }           /* 精确匹配 */
a[href^="https"] { }             /* 以 https 开头 */
img[src$=".png"] { }             /* 以 .png 结尾 */
[class*="btn"] { }               /* 包含 btn */

/* === 伪类选择器（重点！） === */
a:hover { }              /* 鼠标悬停 */
a:active { }             /* 按下瞬间 */
a:focus { }              /* 获得焦点（键盘导航） */
input:focus-visible { }  /* 仅键盘聚焦时显示（推荐） */
li:first-child { }       /* 第一个子元素 */
li:last-child { }        /* 最后一个子元素 */
li:nth-child(2n) { }     /* 偶数位子元素 */
li:nth-child(odd) { }    /* 奇数位子元素 */
:not(.disabled) { }      /* 排除选择 */
:is(h1, h2, h3) { }     /* 匹配任一（减少重复） */
:has(.icon) { }          /* 父选择器（2023 新增，超有用！）

/* === 伪元素选择器 === */
p::before { content: ">> "; }   /* 元素前插入内容 */
p::after { content: "<<"; }     /* 元素后插入内容 */
p::first-line { }               /* 第一行 */
p::first-letter { }             /* 首字母 */
::selection { }                 /* 用户选中的文本 */

/* === CSS 变量（自定义属性） === */
:root {
  --primary-color: #3b82f6;
  --font-size-base: 16px;
  --spacing: 8px;
}
.button {
  background: var(--primary-color);
  padding: calc(var(--spacing) * 2);
}
```

**3. 盒模型（Box Model — 前端最核心概念之一）**

```
┌─────────────────────────────────────────┐
│              margin（外边距）              │
│  ┌───────────────────────────────────┐  │
│  │          border（边框）             │  │
│  │  ┌─────────────────────────────┐  │  │
│  │  │       padding（内边距）       │  │  │
│  │  │  ┌─────────────────────┐    │  │  │
│  │  │  │                     │    │  │  │
│  │  │  │    content（内容）    │    │  │  │
│  │  │  │                     │    │  │  │
│  │  │  └─────────────────────┘    │  │  │
│  │  └─────────────────────────────┘  │  │
│  └───────────────────────────────────┘  │
└─────────────────────────────────────────┘
```

```css
/* ★★★ 关键：box-sizing ★★★ */
/* 默认 content-box：width 只算内容，padding/border 额外增加 */
/* 推荐 border-box：width = content + padding + border */

/* 全局设置（必加！） */
*, *::before, *::after {
  box-sizing: border-box;
}

/* 举例说明 */
.box-content {
  box-sizing: content-box;
  width: 200px;       /* 内容宽 200px */
  padding: 20px;      /* 实际占 240px */
  border: 1px solid;  /* 实际占 242px */
}

.box-border {
  box-sizing: border-box;
  width: 200px;       /* 总宽 200px（内容自动缩为 158px） */
  padding: 20px;
  border: 1px solid;
}
```

**4. 尺寸与单位**

```css
/* 绝对单位 */
width: 200px;    /* 像素 — 最常用 */
width: 2rem;     /* 1rem = 根元素 font-size（默认 16px）→ 32px */
width: 1.5em;    /* 1em = 当前元素 font-size */

/* 相对单位 */
width: 50%;      /* 父元素宽度的 50% */
width: 100vw;    /* 视口宽度的 100% */
height: 100vh;   /* 视口高度的 100% */
width: 10ch;     /* 字符 '0' 的 10 倍宽（适合输入框） */
width: min(300px, 50%);  /* 取较小值 — 响应式利器 */
width: max(200px, 80%);  /* 取较大值 */
width: clamp(200px, 50%, 800px); /* 夹紧在 200px-800px 之间 */
```

**5. 层叠与优先级（Specificity）**

```
优先级从高到低：
1. !important（尽量避免使用）
2. 内联样式 style="..."
3. #id 选择器
4. .class / [attr] / :pseudo-class
5. 元素选择器 / ::pseudo-element
6. 通配符 *

记忆口诀：内联 > ID > 类 > 标签

同优先级时：后定义的覆盖先定义的（后端类比：后面的 middleware 覆盖前面的）
```

#### 实战练习

1. **盒模型计算题**：给定一个 `border-box` 的 div，width=300px，padding=20px，border=2px，问内容区宽度是多少？（答案：256px）
2. **用 CSS 变量做一个主题切换**：定义 `--bg-color`、`--text-color` 等变量，通过 JS 切换 `:root` 上的变量值实现暗色/亮色主题
3. **选择器挑战**：用最少的 CSS 规则样式化一个复杂的嵌套列表

---

### Day 3：Flexbox 弹性布局

#### 学习内容

> **后端类比**：Flexbox 就像是一个智能的容器编排系统，你告诉容器"这些子元素怎么排列"，容器自动计算位置。类似 Go 中 channel 的缓冲区管理——自动调度。

**1. 容器属性（设在父元素上）**

```css
.container {
  display: flex;
  
  /* 主轴方向（默认 row，从左到右） */
  flex-direction: row;          /* → 水平从左到右 */
  flex-direction: row-reverse;  /* ← 水平从右到左 */
  flex-direction: column;       /* ↓ 垂直从上到下 */
  flex-direction: column-reverse;/* ↑ 垂直从下到上 */
  
  /* 换行（默认 nowrap） */
  flex-wrap: wrap;              /* 超出时换行 */
  flex-wrap: wrap-reverse;      /* 反向换行 */
  
  /* 主轴对齐（默认 flex-start） */
  justify-content: flex-start;  /* 左对齐 */
  justify-content: center;      /* 居中 ★ 最常用 */
  justify-content: flex-end;    /* 右对齐 */
  justify-content: space-between; /* 两端对齐，中间等分 */
  justify-content: space-around;  /* 每项两侧等分 */
  justify-content: space-evenly;  /* 完全等分 */
  
  /* 交叉轴对齐（默认 stretch） */
  align-items: stretch;         /* 拉伸填满（默认） */
  align-items: center;          /* 居中 ★ 最常用 */
  align-items: flex-start;      /* 顶部对齐 */
  align-items: flex-end;        /* 底部对齐 */
  align-items: baseline;        /* 文字基线对齐 */
  
  /* 多行对齐 */
  align-content: center;        /* 多行整体居中 */
  
  /* 间距（2024 新增，替代 gap） */
  gap: 16px;                    /* 行列间距相同 */
  gap: 16px 8px;                /* 行间距16px 列间距8px */
}
```

**2. 子元素属性（设在子元素上）**

```css
.item {
  /* 弹性增长因子（分配剩余空间） */
  flex-grow: 1;     /* 等分剩余空间 */
  flex-grow: 2;     /* 占 2 份 */
  
  /* 弹性收缩因子（空间不够时如何缩小） */
  flex-shrink: 0;   /* 不缩小（固定宽度元素常用） */
  flex-shrink: 1;   /* 默认，等比缩小 */
  
  /* 基础大小 */
  flex-basis: 200px; /* 初始宽度 200px */
  flex-basis: auto;  /* 由内容/width 决定 */
  
  /* 简写（★★★ 最常用 ★★★） */
  flex: 1;            /* flex: 1 1 0% — 等分 */
  flex: 0 0 200px;    /* 固定 200px，不伸缩 */
  flex: 1 1 auto;     /* 可伸缩，按内容比例 */
  
  /* 单独交叉轴对齐 */
  align-self: center;  /* 这一项单独居中 */
  align-self: flex-end;
  
  /* 排序 */
  order: -1;   /* 排到最前面 */
  order: 1;    /* 排到最后面 */
}
```

**3. 经典布局模式**

```css
/* ★ 水平垂直居中（最常用） */
.center-box {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

/* ★ 导航栏：Logo 在左，菜单在右 */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 24px;
}

/* ★ 等宽多列布局 */
.columns {
  display: flex;
  gap: 16px;
}
.columns > * {
  flex: 1;  /* 每列等宽 */
}

/* ★ 底部固定 Footer（sticky footer） */
.page {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
.page main {
  flex: 1;  /* 主内容区撑满 */
}
.page footer {
  /* footer 自然在底部 */
}

/* ★ 卡片内图标+文字 */
.card-action {
  display: flex;
  align-items: center;
  gap: 8px;
}
```

#### 实战练习

1. **用纯 Flexbox 还原一个导航栏**：Logo 左侧，导航链接居中，登录按钮右侧
2. **做一个响应式卡片网格**：大屏 4 列，中屏 2 列，小屏 1 列（用 `flex-wrap` + 百分比宽度）
3. **经典面试题**：用 Flexbox 实现圣杯布局（header + 左侧边栏 + 主内容 + 右侧边栏 + footer）

---

### Day 4：CSS Grid 网格布局

#### 学习内容

> **后端类比**：Grid 就像二维数组/矩阵，你可以精确定义行列。Flexbox 是一维的（行或列），Grid 是二维的（行和列同时控制）。

**1. 容器属性**

```css
.grid {
  display: grid;
  
  /* 定义列 */
  grid-template-columns: 200px 1fr 200px;     /* 三列：固定-弹性-固定 */
  grid-template-columns: repeat(3, 1fr);       /* 三等列 */
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr)); /* 自适应列数 ★★★ */
  
  /* 定义行 */
  grid-template-rows: 60px 1fr 40px;           /* 三行：固定-弹性-固定 */
  grid-template-rows: auto 1fr auto;
  
  /* 间距 */
  gap: 16px;
  row-gap: 16px;
  column-gap: 24px;
  
  /* 对齐 */
  justify-items: center;   /* 水平居中所有子元素 */
  align-items: center;     /* 垂直居中所有子元素 */
  place-items: center;     /* 简写 ★ */
  
  justify-content: center; /* 整个网格居中 */
  align-content: center;
  place-content: center;   /* 简写 */
}

/* ★★★ 命名区域（最直观的布局方式） ★★★ */
.layout {
  display: grid;
  grid-template-areas:
    "header header header"
    "sidebar main aside"
    "footer footer footer";
  grid-template-columns: 250px 1fr 200px;
  grid-template-rows: 60px 1fr 50px;
  min-height: 100vh;
}
.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.aside   { grid-area: aside; }
.footer  { grid-area: footer; }
```

**2. 子元素属性**

```css
.item {
  /* 跨列/跨行 */
  grid-column: 1 / 3;       /* 从第1条线到第3条线（占2列） */
  grid-column: span 2;      /* 跨2列 */
  grid-row: 1 / 3;          /* 跨2行 */
  
  /* 命名区域 */
  grid-area: header;
  
  /* 对齐 */
  justify-self: end;        /* 单个元素右对齐 */
  align-self: center;
  place-self: center end;   /* 简写 */
}
```

**3. Grid vs Flexbox 选择指南**

| 场景 | 推荐 | 原因 |
|------|------|------|
| 一维排列（导航、列表） | Flexbox | 单方向控制足够 |
| 二维布局（表格、仪表盘） | Grid | 行列同时控制 |
| 内容驱动的等宽卡片 | Flexbox wrap | 自动换行 |
| 精确的页面框架 | Grid | grid-template-areas |
| 对齐单个元素 | 都可以 | Flexbox 更简单 |

#### 实战练习

1. **用 Grid 还原一个 Dashboard 布局**：顶部统计卡片行（4列），中间图表区（2:1分栏），底部表格区
2. **用 `repeat(auto-fill, minmax())` 做一个自适应图片画廊**：自动根据屏幕宽度调整列数
3. **Grid + Flexbox 混合使用**：Grid 做页面整体布局，Flexbox 做每个区块内部排列

---

### Day 5：响应式设计与移动端适配

#### 学习内容

**1. 媒体查询（Media Queries）**

```css
/* 移动优先（Mobile First）— 推荐！ */
/* 默认写移动端样式，然后用 min-width 逐步增强 */

/* 基础（移动端，<768px） */
.container {
  padding: 16px;
  font-size: 14px;
}

/* 平板（>=768px） */
@media (min-width: 768px) {
  .container {
    padding: 24px;
    font-size: 16px;
  }
}

/* 桌面（>=1024px） */
@media (min-width: 1024px) {
  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 32px;
  }
}

/* 大屏（>=1440px） */
@media (min-width: 1440px) {
  .container {
    max-width: 1400px;
  }
}

/* 桌面优先（不推荐，但会遇到） */
@media (max-width: 767px) {
  /* 移动端覆盖样式 */
}

/* 其他媒体特性 */
@media (prefers-color-scheme: dark) { }    /* 暗色模式 */
@media (prefers-reduced-motion: reduce) { } /* 减少动画 */
@media (print) { }                          /* 打印样式 */
@media (hover: hover) { }                   /* 支持悬停的设备 */
```

**2. 响应式图片**

```html
<picture>
  <!-- 小屏用小图 -->
  <source media="(max-width: 600px)" srcset="img-small.webp" type="image/webp">
  <source media="(max-width: 600px)" srcset="img-small.jpg">
  <!-- 大屏用大图 -->
  <source srcset="img-large.webp" type="image/webp">
  <source srcset="img-large.jpg">
  <!-- 降级 -->
  <img src="img-large.jpg" alt="描述" loading="lazy">
</picture>
```

**3. 移动端特殊处理**

```css
/* 触摸友好的按钮（最小 44x44px） */
button, .btn {
  min-height: 44px;
  min-width: 44px;
  padding: 12px 24px;
}

/* 防止文字选择（移动端长按） */
.no-select {
  -webkit-user-select: none;
  user-select: none;
}

/* 安全区域（刘海屏） */
body {
  padding: env(safe-area-inset-top) env(safe-area-inset-right) 
           env(safe-area-inset-bottom) env(safe-area-inset-left);
}

/* 隐藏滚动条但保留滚动功能 */
.hide-scrollbar {
  -ms-overflow-style: none;
  scrollbar-width: none;
}
.hide-scrollbar::-webkit-scrollbar {
  display: none;
}

/* 移动端 1px 边框（Retina 屏适配） */
.border-1px {
  position: relative;
}
.border-1px::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 1px;
  background: #ddd;
  transform: scaleY(0.5);  /* 缩小一半，在 Retina 上显示为 0.5px */
}
```

**4. 视口与缩放**

```html
<!-- 必须加！否则移动端会缩放到 980px 宽 -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=5.0">
```

**5. 常见断点（Breakpoints）**

| 名称 | 宽度 | 设备 |
|------|------|------|
| sm | >= 640px | 大手机/小平板 |
| md | >= 768px | 平板 |
| lg | >= 1024px | 笔记本 |
| xl | >= 1280px | 桌面 |
| 2xl | >= 1536px | 大屏桌面 |

#### 实战练习

1. **做一个完整的响应式页面**：手机端单列、平板双列、桌面三列，导航栏在手机端变成汉堡菜单
2. **实现暗色模式切换**：用 `prefers-color-scheme` + CSS 变量 + JS 手动切换
3. **测试**：用 Chrome DevTools 的设备模拟器（Ctrl+Shift+M）在各种设备上测试

---

### Day 6：CSS 动画与过渡 + 第一周项目

#### 学习内容

**1. CSS 过渡（Transition）**

```css
/* 基础语法 */
.button {
  background: #3b82f6;
  color: white;
  transition: all 0.3s ease;
}
.button:hover {
  background: #2563eb;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(59, 130, 246, 0.4);
}

/* 分别指定属性 */
.card {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

/* 缓动函数 */
transition-timing-function: ease;        /* 默认 */
transition-timing-function: linear;      /* 匀速 */
transition-timing-function: ease-in;     /* 慢入 */
transition-timing-function: ease-out;    /* 慢出 */
transition-timing-function: ease-in-out; /* 慢入慢出 */
transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1); /* 自定义贝塞尔曲线 */
```

**2. CSS 动画（Animation）**

```css
/* 定义动画 */
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

@keyframes slideIn {
  0% { transform: translateX(-100%); opacity: 0; }
  100% { transform: translateX(0); opacity: 1; }
}

/* 使用动画 */
.fade-in {
  animation: fadeIn 0.5s ease-out;
}

.spinner {
  animation: spin 1s linear infinite;  /* 无限循环 */
}

/* 动画控制 */
.animated {
  animation: fadeIn 0.5s ease-out forwards; /* forwards 保持最终状态 */
  animation-delay: 0.2s;                    /* 延迟 */
  animation-iteration-count: 3;              /* 重复次数 */
  animation-direction: alternate;            /* 交替反向 */
  animation-fill-mode: both;                 /* 延迟期间也应用初始样式 */
}
```

**3. Transform 变换**

```css
.transform-demo {
  /* 平移 */
  transform: translateX(100px);
  transform: translateY(-50px);
  transform: translate(50%, -50%); /* 相对于自身尺寸 */

  /* 旋转 */
  transform: rotate(45deg);

  /* 缩放 */
  transform: scale(1.5);
  transform: scaleX(2);

  /* 倾斜 */
  transform: skew(10deg, 5deg);

  /* 组合（注意顺序影响结果！） */
  transform: translateX(50%) rotate(45deg) scale(1.2);

  /* 性能提示：只触发 composite，不触发 layout/paint */
  will-change: transform, opacity;
}
```

**4. 性能优化**

```css
/* ★ 只动画 transform 和 opacity（GPU 加速） */
.good-animation {
  transition: transform 0.3s, opacity 0.3s;
}

/* ✗ 避免动画这些属性（触发重排，性能差） */
.bad-animation {
  transition: width 0.3s, height 0.3s, top 0.3s, left 0.3s;
}

/* 减少动画（无障碍） */
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

#### 第一周项目：个人作品集网站

**需求**：
- 响应式布局（手机/平板/桌面）
- 导航栏（滚动时固定顶部，背景模糊）
- Hero 区域（大标题 + 副标题 + CTA 按钮 + 入场动画）
- 关于我（头像 + 文字介绍）
- 技能展示（进度条动画）
- 项目展示（卡片网格 + hover 效果）
- 联系表单（带验证）
- Footer
- 暗色模式切换
- 滚动动画（IntersectionObserver）

**技术要求**：
- 纯 HTML + CSS（不用 JS 框架）
- 用 CSS 变量管理主题色
- Flexbox + Grid 混合布局
- CSS 动画和过渡
- 响应式设计

---

## 第二周：JavaScript 深度精讲

> **本周目标**：深入理解 JavaScript 语言核心，掌握 ES6+ 现代语法、异步编程、DOM 操作、事件系统
> **后端类比**：JS 的原型链 ≈ Go 的结构体嵌入；闭包 ≈ Go 的闭包；Promise ≈ Go 的 channel；事件循环 ≈ Go 的 runtime scheduler

---

### Day 7：JavaScript 基础与类型系统

#### 学习内容

**1. 变量声明（★★★ 重点理解区别）**

```javascript
// var — 函数作用域，变量提升（避免使用！）
function example() {
  console.log(x); // undefined（不会报错，因为变量提升）
  var x = 10;
}

// let — 块级作用域，暂时性死区（推荐）
function example() {
  // console.log(x); // ReferenceError!
  let x = 10;
  if (true) {
    let y = 20; // 只在 if 块内可见
  }
  // console.log(y); // ReferenceError!
}

// const — 块级作用域，必须初始化，不能重新赋值（推荐）
const PI = 3.14;
// PI = 3; // TypeError!

// ⚠️ const 不是不可变！对象/数组的属性可以修改
const arr = [1, 2, 3];
arr.push(4);      // ✅ 可以
arr = [5, 6];     // ❌ TypeError!

const obj = { name: 'Alice' };
obj.name = 'Bob'; // ✅ 可以
obj = {};         // ❌ TypeError!

// 后端类比：
// let ≈ Go 的 :=（短变量声明）
// const ≈ Go 的 const（但更灵活）
// var ≈ 没有对应（Go 没有变量提升这种概念）
```

**2. 数据类型**

```javascript
// === 原始类型（Primitive）===
typeof 42;           // "number"
typeof "hello";      // "string"
typeof true;         // "boolean"
typeof undefined;    // "undefined"
typeof null;         // "object" ← 历史遗留 bug！用 === null 判断
typeof Symbol();     // "symbol"
typeof 42n;          // "bigint"
typeof function(){}; // "function" ← 不是原始类型，但 typeof 返回这个

// === 引用类型 ===
typeof {};           // "object"
typeof [];           // "object" ← 数组也是对象！用 Array.isArray() 判断
typeof null;         // "object" ← 又是这个 bug

// === 类型转换陷阱（★★★ 面试高频）===
// 隐式转换规则：
"5" + 3;     // "53"（字符串拼接）
"5" - 3;     // 2（数学运算）
"5" * 3;     // 15
"5" == 5;    // true（宽松相等，会类型转换）
"5" === 5;   // false（严格相等，推荐！）
null == undefined;  // true
null === undefined; // false
[] == false;  // true（各种隐式转换...）
[] == ![];    // true（经典面试题）

// ★ 永远用 === 严格相等！
```

**3. 解构赋值（ES6+）**

```javascript
// 数组解构
const [a, b, c] = [1, 2, 3];
const [first, ...rest] = [1, 2, 3, 4]; // first=1, rest=[2,3,4]
const [, second] = [1, 2, 3];          // 跳过第一个

// 对象解构
const { name, age } = { name: 'Alice', age: 30 };
const { name: userName, age: userAge } = obj; // 重命名
const { name = 'default' } = {};       // 默认值

// 嵌套解构
const { address: { city, zip } } = user;

// 函数参数解构（★★★ 超常用）
function createUser({ name, age, role = 'user' }) {
  return { name, age, role };
}
createUser({ name: 'Alice', age: 30 });

// 后端类比：类似 Go 的多重赋值，但更灵活
// Go: a, b := 1, 2
// JS: const [a, b] = [1, 2]
```

**4. 展开运算符（Spread / Rest）**

```javascript
// 数组展开
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5]; // [1,2,3,4,5]
const merged = [...arr1, ...arr2];

// 对象展开（浅拷贝）
const defaults = { theme: 'light', lang: 'zh', debug: false };
const userConfig = { theme: 'dark', lang: 'en' };
const config = { ...defaults, ...userConfig };
// { theme: 'dark', lang: 'en', debug: false }

// Rest 参数
function sum(...numbers) {
  return numbers.reduce((acc, n) => acc + n, 0);
}
sum(1, 2, 3, 4); // 10

// 后端类比：展开运算符 ≈ Go 的 ... 操作符
```

**5. 模板字符串**

```javascript
const name = 'Alice';
const age = 30;

// 基础
const greeting = `你好，${name}！你今年 ${age} 岁。`;

// 表达式
const info = `${name} 是${age >= 18 ? '成年' : '未成年'}人`;

// 多行
const html = `
  <div class="card">
    <h2>${name}</h2>
    <p>年龄：${age}</p>
  </div>
`;

// 标签模板（高级用法）
function highlight(strings, ...values) {
  return strings.reduce((result, str, i) => {
    return result + str + (values[i] ? `<mark>${values[i]}</mark>` : '');
  }, '');
}
highlight`搜索 ${keyword} 的结果`; // keyword 会被 <mark> 包裹
```

#### 实战练习

1. **类型判断函数**：写一个 `deepTypeOf(value)` 函数，能正确区分 `null`、`[]`、`{}`、`Date`、`RegExp` 等
2. **解构练习**：从 API 返回的嵌套 JSON 中提取特定字段
3. **对象合并工具**：实现一个 `deepMerge(target, ...sources)` 深合并函数

---

### Day 8：函数、作用域与闭包

#### 学习内容

**1. 函数定义方式**

```javascript
// 函数声明（有提升）
function add(a, b) { return a + b; }

// 函数表达式（无提升）
const add = function(a, b) { return a + b; };

// 箭头函数（★★★ 最常用）
const add = (a, b) => a + b;
const square = x => x * x;
const getObj = () => ({ key: 'value' }); // 返回对象要加括号

// 箭头函数 vs 普通函数的区别：
// 1. 没有 this 绑定（继承外层 this）
// 2. 没有 arguments 对象
// 3. 不能用作构造函数（不能 new）
// 4. 没有 prototype 属性

// ★ 后端类比：箭头函数 ≈ Go 的匿名函数
// Go: func(x int) int { return x * x }
// JS: x => x * x
```

**2. 默认参数与剩余参数**

```javascript
// 默认参数
function fetch(url, method = 'GET', headers = {}) {
  // ...
}
fetch('/api/users');           // method='GET', headers={}
fetch('/api/users', 'POST');   // headers={}

// 剩余参数
function log(level, ...messages) {
  console.log(`[${level}]`, ...messages);
}
log('INFO', '请求开始', 'URL:', url);

// 后端类比：类似 Go 的可变参数
// Go: func log(level string, msgs ...string)
```

**3. 作用域链**

```javascript
// 全局作用域
let globalVar = 'global';

function outer() {
  // 函数作用域
  let outerVar = 'outer';
  
  function inner() {
    // 内层函数作用域
    let innerVar = 'inner';
    
    console.log(innerVar);  // ✅ 'inner'
    console.log(outerVar);  // ✅ 'outer'（沿作用域链向上查找）
    console.log(globalVar); // ✅ 'global'
  }
  
  inner();
  // console.log(innerVar); // ❌ ReferenceError
}

outer();
// 后端类比：类似 Go 的作用域规则，但 JS 有函数作用域（Go 只有块作用域）
```

**4. 闭包（Closure — ★★★ 核心概念）**

```javascript
// 闭包 = 函数 + 它能访问的外层变量
function createCounter() {
  let count = 0; // 被闭包"捕获"的变量
  
  return {
    increment: () => ++count,
    decrement: () => --count,
    getCount: () => count,
  };
}

const counter = createCounter();
counter.increment(); // 1
counter.increment(); // 2
counter.getCount();  // 2
// count 变量在外部无法直接访问，只能通过返回的方法操作
// ★ 这就是"数据私有化"——类似 Go 的私有字段

// 实际应用：防抖（Debounce）
function debounce(fn, delay) {
  let timer = null;
  return function(...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}
const search = debounce(query => fetchResults(query), 300);
input.addEventListener('input', e => search(e.target.value));

// 实际应用：节流（Throttle）
function throttle(fn, interval) {
  let lastTime = 0;
  return function(...args) {
    const now = Date.now();
    if (now - lastTime >= interval) {
      lastTime = now;
      fn.apply(this, args);
    }
  };
}
const onScroll = throttle(() => updatePosition(), 100);
window.addEventListener('scroll', onScroll);

// 实际应用：缓存（Memoize）
function memoize(fn) {
  const cache = new Map();
  return function(...args) {
    const key = JSON.stringify(args);
    if (cache.has(key)) return cache.get(key);
    const result = fn.apply(this, args);
    cache.set(key, result);
    return result;
  };
}
const expensiveCalc = memoize(n => {
  console.log('计算中...');
  return n * n;
});
expensiveCalc(5); // "计算中..." → 25
expensiveCalc(5); // 25（直接从缓存取）

// 后端类比：
// 闭包 ≈ Go 的闭包（概念相同）
// 防抖 ≈ Go 中带 timer 的 rate limiter
// 节流 ≈ Go 中 time.Ticker
// 缓存 ≈ sync.Map 或带锁的 map
```

**5. this 关键字（★★★ JS 最令人困惑的概念）**

```javascript
// this 的值取决于函数如何被调用（不是定义位置！）

// 1. 全局上下文
console.log(this); // window（浏览器）/ global（Node）

// 2. 对象方法
const user = {
  name: 'Alice',
  greet() {
    console.log(this.name); // 'Alice' — this 指向调用对象
  }
};
user.greet(); // 'Alice'

// 3. 箭头函数（继承外层 this）
const user = {
  name: 'Alice',
  greet: () => {
    console.log(this.name); // undefined — this 不指向 user！
  },
  greetLater() {
    setTimeout(() => {
      console.log(this.name); // 'Alice' — 箭头函数继承 greetLater 的 this
    }, 100);
  }
};

// 4. 回调函数中的 this 丢失
class Button {
  constructor(label) {
    this.label = label;
  }
  // ❌ 错误：this 丢失
  // onClick() { console.log(this.label); }
  
  // ✅ 方案1：箭头函数
  onClick = () => console.log(this.label);
  
  // ✅ 方案2：bind
  // constructor() { this.onClick = this.onClick.bind(this); }
}

// 5. 显式绑定
function greet(greeting) {
  console.log(`${greeting}, ${this.name}`);
}
greet.call({ name: 'Alice' }, 'Hello');  // "Hello, Alice"
greet.apply({ name: 'Bob' }, ['Hi']);     // "Hi, Bob"
const boundGreet = greet.bind({ name: 'Charlie' });
boundGreet('Hey'); // "Hey, Charlie"

// 后端类比：
// JS 的 this ≈ Go 的 receiver（方法接收者）
// 但 JS 的 this 更灵活（也更混乱），Go 的 receiver 是编译时确定的
```

#### 实战练习

1. **实现一个 EventEmitter**：支持 `on`、`off`、`emit`、`once` 方法
2. **实现 curry 函数**：`curry(add)(1)(2)` → `3`
3. **实现 compose 函数**：`compose(fn1, fn2, fn3)(x)` → `fn1(fn2(fn3(x)))`

---

### Day 9：原型链与面向对象

#### 学习内容

**1. 原型链（Prototype Chain — JS 的继承机制）**

```javascript
// 每个对象都有一个内部属性 [[Prototype]]
// 通过 __proto__ 或 Object.getPrototypeOf() 访问
// 通过 Object.create() 设置

// 原型链查找过程：
const arr = [1, 2, 3];
arr.hasOwnProperty('length'); // false
// 查找顺序：arr 自身 → Array.prototype → Object.prototype → null

// Array.prototype 上有：push, pop, map, filter, reduce...
// Object.prototype 上有：toString, hasOwnProperty, valueOf...

// ★ 经典图解：
// arr → Array.prototype → Object.prototype → null
//   (push, map...)    (toString...)      (终点)

// 后端类比：
// 原型链 ≈ Go 的结构体嵌入（embedding）
// type Animal struct { Name string }
// type Dog struct { Animal }  // Dog 继承 Animal 的方法
// 但 JS 的原型链是运行时的，Go 的嵌入是编译时的
```

**2. ES6 Class（语法糖）**

```javascript
// ES6 class 本质上是构造函数 + 原型链的语法糖
class Animal {
  // 构造函数
  constructor(name) {
    this.name = name;
  }
  
  // 实例方法（挂在原型上）
  speak() {
    console.log(`${this.name} makes a sound.`);
  }
  
  // 静态方法（挂在类上，类似 Go 的包级函数）
  static create(name) {
    return new Animal(name);
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name); // 调用父类构造函数（必须！）
    this.breed = breed;
  }
  
  // 重写父类方法
  speak() {
    console.log(`${this.name} barks!`);
  }
  
  // 新方法
  fetch(item) {
    console.log(`${this.name} fetches the ${item}.`);
  }
}

const dog = new Dog('Rex', 'German Shepherd');
dog.speak();   // "Rex barks!"
dog.fetch('ball'); // "Rex fetches the ball."
dog instanceof Dog;    // true
dog instanceof Animal; // true

// Getter / Setter
class User {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
  
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
  
  set fullName(name) {
    const [first, last] = name.split(' ');
    this.firstName = first;
    this.lastName = last;
  }
}

// 私有字段（2022+）
class BankAccount {
  #balance = 0; // # 开头表示私有字段
  
  deposit(amount) {
    if (amount > 0) this.#balance += amount;
  }
  
  get balance() {
    return this.#balance;
  }
}

// 后端类比：
// class ≈ Go 的 struct + 方法集
// extends ≈ Go 的嵌入
// private fields ≈ Go 的小写字母私有字段
// getter/setter ≈ Go 没有对应（Go 不推荐 getter/setter）
```

**3. 常用内置对象方法**

```javascript
// === Object 静态方法 ===
Object.keys(obj);           // 获取所有键
Object.values(obj);         // 获取所有值
Object.entries(obj);        // 获取键值对数组
Object.assign(target, src); // 浅合并
Object.freeze(obj);         // 冻结（不可修改）
Object.seal(obj);           // 密封（不可添加/删除属性）

// === 数组高阶方法（★★★ 每天都在用）===
const users = [
  { name: 'Alice', age: 30, role: 'admin' },
  { name: 'Bob', age: 25, role: 'user' },
  { name: 'Charlie', age: 35, role: 'admin' },
];

// map — 映射转换（类似 Go 没有直接对应，需要 for range）
const names = users.map(u => u.name); // ['Alice', 'Bob', 'Charlie']

// filter — 过滤
const admins = users.filter(u => u.role === 'admin');

// find — 查找第一个匹配
const bob = users.find(u => u.name === 'Bob');

// some — 是否存在匹配
const hasAdmin = users.some(u => u.role === 'admin'); // true

// every — 是否全部匹配
const allAdults = users.every(u => u.age >= 18); // true

// reduce — 累积计算（★★★ 超强大）
const totalAge = users.reduce((sum, u) => sum + u.age, 0); // 90
const grouped = users.reduce((acc, u) => {
  (acc[u.role] = acc[u.role] || []).push(u);
  return acc;
}, {}); // { admin: [...], user: [...] }

// flatMap — 映射 + 扁平化
const nested = [[1, 2], [3, 4], [5]];
nested.flat();           // [1,2,3,4,5]
users.flatMap(u => u.hobbies || []); // 扁平化获取所有爱好

// sort — 排序（注意：原地修改！）
users.sort((a, b) => a.age - b.age); // 按年龄升序
[3, 1, 2].sort((a, b) => a - b);    // [1, 2, 3]

// 后端类比：
// map ≈ 遍历 slice 生成新 slice
// filter ≈ 遍历 slice 过滤
// reduce ≈ 遍历 slice 累积（Go 没有内置，需要手写）
// find ≈ 遍历 slice 查找
```

#### 实战练习

1. **实现一个简易的 ORM**：用 class + 原型链实现 `Model.find()`、`Model.where()`、`Model.first()` 链式调用
2. **数组方法练习**：用 `reduce` 实现 `map`、`filter`、`groupBy`、`uniq`、`flatten`
3. **深拷贝函数**：实现 `deepClone(obj)`，处理循环引用

---

### Day 10：异步编程（Promise / async-await）

#### 学习内容

> **这是前端最重要的概念之一！** 后端工程师必须彻底理解事件循环。

**1. 回调地狱 → Promise → async/await**

```javascript
// ❌ 回调地狱（Callback Hell）
getUser(id, (user) => {
  getOrders(user.id, (orders) => {
    getOrderDetail(orders[0].id, (detail) => {
      getProduct(detail.productId, (product) => {
        console.log(product);
      });
    });
  });
});

// ✅ Promise 链
getUser(id)
  .then(user => getOrders(user.id))
  .then(orders => getOrderDetail(orders[0].id))
  .then(detail => getProduct(detail.productId))
  .then(product => console.log(product))
  .catch(err => console.error(err));

// ✅✅ async/await（最推荐 — 看起来像同步代码）
async function showProduct(id) {
  try {
    const user = await getUser(id);
    const orders = await getOrders(user.id);
    const detail = await getOrderDetail(orders[0].id);
    const product = await getProduct(detail.productId);
    console.log(product);
  } catch (err) {
    console.error(err);
  }
}

// 后端类比：
// 回调 ≈ Go 的 callback 模式（早期 RPC）
// Promise ≈ Go 的 channel（都可以 .then 等待结果）
// async/await ≈ Go 的 goroutine + channel（看起来都是顺序代码）
// 但！Go 是真并行（多线程），JS 是伪并行（单线程事件循环）
```

**2. Promise 详解**

```javascript
// 创建 Promise
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

function fetchUser(id) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (id > 0) {
        resolve({ id, name: 'Alice' });
      } else {
        reject(new Error('Invalid ID'));
      }
    }, 1000);
  });
}

// Promise 状态：pending → fulfilled / rejected（不可逆）

// 静态方法
Promise.all([p1, p2, p3]);       // 全部成功才成功（并行）
Promise.allSettled([p1, p2, p3]); // 全部完成（不管成功失败）
Promise.race([p1, p2]);          // 第一个完成的结果
Promise.any([p1, p2]);           // 第一个成功的结果

// 并行请求（★★★ 实际开发最常用）
async function loadDashboard() {
  const [user, orders, notifications] = await Promise.all([
    fetchUser(1),
    fetchOrders(1),
    fetchNotifications(1),
  ]);
  // 三个请求并行执行，总时间 = 最慢的那个
}

// 后端类比：
// Promise.all ≈ Go 的 errgroup.Group（WaitGroup）
// Promise.race ≈ Go 的 select + channel
// Promise.allSettled ≈ 没有直接对应（Go 需要自己实现）
```

**3. 事件循环（Event Loop — ★★★ 必须理解）**

```javascript
console.log('1'); // 同步

setTimeout(() => {
  console.log('2'); // 宏任务（Macrotask）
}, 0);

Promise.resolve().then(() => {
  console.log('3'); // 微任务（Microtask）
});

console.log('4'); // 同步

// 输出顺序：1, 4, 3, 2
// 原因：
// 1. 执行同步代码 → 输出 1, 4
// 2. 清空微任务队列 → 输出 3
// 3. 取一个宏任务执行 → 输出 2

// ★ 事件循环执行顺序：
// 同步代码 → 微任务 → 渲染 → 宏任务 → 微任务 → 渲染 → ...

// 宏任务（Macrotask）：setTimeout, setInterval, I/O, UI rendering
// 微任务（Microtask）：Promise.then, MutationObserver, queueMicrotask

// 后端类比：
// 事件循环 ≈ Go 的 runtime scheduler
// 但 Go 有 M:N 调度（多线程），JS 是单线程
// 微任务 ≈ Go 中更高优先级的 goroutine

// ★ 经典面试题
async function async1() {
  console.log('async1 start');
  await async2();
  console.log('async1 end');
}
async function async2() {
  console.log('async2');
}
console.log('script start');
setTimeout(() => console.log('setTimeout'), 0);
async1();
console.log('script end');

// 输出：script start, async1 start, async2, script end, async1 end, setTimeout
```

**4. 实用异步模式**

```javascript
// 带超时的请求
function fetchWithTimeout(url, timeout = 5000) {
  return Promise.race([
    fetch(url),
    new Promise((_, reject) =>
      setTimeout(() => reject(new Error('Timeout')), timeout)
    ),
  ]);
}

// 重试机制
async function fetchWithRetry(url, retries = 3, delay = 1000) {
  for (let i = 0; i < retries; i++) {
    try {
      return await fetch(url);
    } catch (err) {
      if (i === retries - 1) throw err;
      await new Promise(r => setTimeout(r, delay * (i + 1))); // 指数退避
    }
  }
}

// 并发控制（限制同时执行的 Promise 数量）
async function asyncPool(limit, items, fn) {
  const results = [];
  const executing = new Set();
  
  for (const item of items) {
    const p = fn(item).then(r => {
      executing.delete(p);
      return r;
    });
    executing.add(p);
    results.push(p);
    
    if (executing.size >= limit) {
      await Promise.race(executing);
    }
  }
  
  return Promise.all(results);
}

// 后端类比：
// 带超时 ≈ Go 的 context.WithTimeout
// 重试 ≈ Go 的 retry 模式
// 并发控制 ≈ Go 的 buffered channel + worker pool
```

#### 实战练习

1. **事件循环预测题**：写出 10 道复杂的事件循环输出题并验证答案
2. **实现一个 async queue**：支持 `enqueue(asyncFn)` 和 `drain()`，按顺序执行
3. **实现 `Promise.all`、`Promise.race`、`Promise.allSettled`**（不用原生 API）

---

### Day 11：DOM 操作与事件系统

#### 学习内容

**1. DOM 查询**

```javascript
// 现代方法（推荐）
document.querySelector('.class');     // 第一个匹配
document.querySelectorAll('.class');  // 所有匹配（NodeList）
document.getElementById('id');         // 按 ID
document.querySelector('[data-id="123"]'); // 属性选择器

// 遍历
element.children;           // 直接子元素（HTMLCollection）
element.parentElement;      // 父元素
element.nextElementSibling; // 下一个兄弟
element.closest('.card');   // 最近的祖先（含自身）★★★ 超有用

// 创建和修改
const div = document.createElement('div');
div.textContent = 'Hello';           // 设置文本（安全，不解析 HTML）
div.innerHTML = '<strong>Hello</strong>'; // 设置 HTML（危险！XSS 风险）
div.classList.add('active', 'card'); // 添加类
div.classList.remove('hidden');
div.classList.toggle('dark');        // 切换类
div.dataset.userId = '123';          // 设置 data-* 属性

// 插入
parent.appendChild(div);             // 末尾追加
parent.prepend(div);                 // 开头插入
parent.insertBefore(div, refChild);  // 在 refChild 前插入
refChild.insertAdjacentElement('afterend', div); // 在元素旁插入

// 删除
div.remove();                        // 删除自身
parent.removeChild(div);             // 父元素删除子元素

// 后端类比：
// DOM 操作 ≈ 操作 JSON 树结构
// querySelector ≈ JSONPath / XPath
// createElement ≈ 构造一个新节点
```

**2. 事件系统**

```javascript
// 事件绑定（推荐 addEventListener）
button.addEventListener('click', handleClick);

// 事件移除（必须传同一个函数引用！）
button.removeEventListener('click', handleClick);

// 事件对象
function handleClick(event) {
  event.target;        // 触发事件的元素
  event.currentTarget; // 绑定事件的元素
  event.preventDefault();  // 阻止默认行为（如 a 标签跳转）
  event.stopPropagation(); // 阻止事件冒泡
  event.type;          // 事件类型 'click'
}

// ★ 事件冒泡与捕获（★★★ 重要）
// 事件传播顺序：捕获阶段（从外到内）→ 目标阶段 → 冒泡阶段（从内到外）
// addEventListener 第三个参数控制：
// false（默认）— 冒泡阶段触发
// true — 捕获阶段触发

// ★ 事件委托（Event Delegation — ★★★ 超重要模式）
// 不要给每个子元素绑定事件，而是绑定在父元素上
document.querySelector('.list').addEventListener('click', (e) => {
  const item = e.target.closest('.list-item'); // 找到最近的列表项
  if (!item) return;
  
  const id = item.dataset.id;
  console.log('点击了:', id);
});

// 后端类比：
// 事件冒泡 ≈ Go 的 context 传播
// 事件委托 ≈ 中间件模式（在入口统一处理，根据路径分发）
```

**3. 常用事件类型**

```javascript
// 鼠标事件
click, dblclick, mouseenter, mouseleave, mousemove, mousedown, mouseup
contextmenu // 右键菜单

// 键盘事件
keydown, keyup, keypress（已废弃）
// keydown 适合检测功能键（Shift, Ctrl, Enter）
// input 适合检测输入内容变化

// 表单事件
input,     // 输入时实时触发（★★★ 最常用）
change,    // 失去焦点或回车时触发
submit,    // 表单提交
focus, blur,
invalid,   // 验证失败

// 滚动与尺寸
scroll, resize
IntersectionObserver // 元素进入视口（替代 scroll 事件，性能更好）

// 触摸事件（移动端）
touchstart, touchmove, touchend

// 拖拽
dragstart, drag, dragend, dragover, drop
```

**4. IntersectionObserver（★★★ 现代替代 scroll 事件）**

```javascript
// 检测元素是否进入视口
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      // 元素进入视口
      entry.target.classList.add('visible');
      observer.unobserve(entry.target); // 只触发一次
    }
  });
}, { threshold: 0.1 }); // 10% 可见时触发

document.querySelectorAll('.animate-on-scroll').forEach(el => {
  observer.observe(el);
});

// 应用场景：
// 1. 懒加载图片
// 2. 无限滚动
// 3. 滚动动画
// 4. 曝光统计

// 后端类比：
// IntersectionObserver ≈ Go 的 watcher 模式
// 你注册一个观察者，当条件满足时自动回调
```

#### 实战练习

1. **实现一个自定义下拉菜单**：点击展开/收起，点击外部关闭（用事件委托 + closest）
2. **实现图片懒加载**：用 IntersectionObserver，图片进入视口时才加载
3. **实现一个简单的 TODO 应用**：纯 DOM 操作，支持增删改查、过滤、本地存储

---

### Day 12：ES Modules 与 Web API + 第二周项目

#### 学习内容

**1. ES Modules（现代模块系统）**

```javascript
// ===== 导出 =====
// math.js
export const PI = 3.14;
export function add(a, b) { return a + b; }
export default class Calculator { /* ... */ }

// 或统一导出
export { PI, add, Calculator };

// ===== 导入 =====
import Calculator, { PI, add } from './math.js';
import * as math from './math.js';

// 动态导入（代码分割）
const module = await import('./heavy-module.js');

// 后端类比：
// ES Modules ≈ Go 的 package/import
// export ≈ Go 的导出（大写字母）
// export default ≈ Go 没有（Go 没有默认导出概念）
// import * ≈ Go 的 . import（不推荐）
```

**2. 常用 Web API**

```javascript
// === Fetch API（HTTP 请求）===
const response = await fetch('/api/users', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ name: 'Alice' }),
});
const data = await response.json();
if (!response.ok) throw new Error(data.message);

// 后端类比：fetch ≈ Go 的 http.Get / http.Post

// === LocalStorage / SessionStorage ===
localStorage.setItem('token', 'abc123');
const token = localStorage.getItem('token');
localStorage.removeItem('token');
localStorage.clear();

// SessionStorage — 关闭标签页就清除
// LocalStorage — 永久保存（除非手动清除）
// Cookie — 每次请求自动携带（有大小限制 4KB）

// === URL API ===
const url = new URL('https://example.com/path?key=value#hash');
url.searchParams.get('key');     // 'value'
url.searchParams.set('page', '2');
url.toString(); // 更新后的 URL

// === History API（SPA 路由基础）===
history.pushState({}, '', '/new-page');  // 添加历史记录
history.replaceState({}, '', '/new-page'); // 替换当前记录
window.addEventListener('popstate', () => {
  // 浏览器前进/后退时触发
});

// === Clipboard API ===
await navigator.clipboard.writeText('复制的内容');
const text = await navigator.clipboard.readText();

// === Geolocation API ===
navigator.geolocation.getCurrentPosition(pos => {
  console.log(pos.coords.latitude, pos.coords.longitude);
});
```

**3. 错误处理**

```javascript
// 全局错误捕获
window.addEventListener('error', (e) => {
  console.error('全局错误:', e.error);
  // 上报到错误监控服务
});

window.addEventListener('unhandledrejection', (e) => {
  console.error('未处理的 Promise 拒绝:', e.reason);
});

// 自定义错误
class AppError extends Error {
  constructor(message, code) {
    super(message);
    this.code = code;
    this.name = 'AppError';
  }
}

// 后端类比：
// 全局错误捕获 ≈ Go 的 recover()
// 自定义错误 ≈ Go 的自定义 error 类型
```

#### 第二周项目：任务管理应用（Kanban Board）

**需求**：
- 三列看板：待办（Todo）、进行中（In Progress）、已完成（Done）
- 支持拖拽卡片在列之间移动（HTML5 Drag & Drop API）
- 添加/编辑/删除任务
- 任务优先级标记（高/中/低）
- 搜索和过滤
- 数据持久化到 LocalStorage
- 拖拽时的视觉反馈动画

**技术要求**：
- 纯 JavaScript（不用框架）
- ES Modules 组织代码
- 自定义事件系统
- LocalStorage 持久化
- CSS 动画和过渡

---

## 第三周：现代前端框架与工程化

> **本周目标**：掌握 React/Vue 核心概念、组件化开发、状态管理、路由、构建工具
> **后端类比**：组件 ≈ 可复用的函数/模块；状态管理 ≈ 内存数据库；路由 ≈ HTTP 路由器；构建工具 ≈ 编译器

---

### Day 13：React 核心概念与 JSX

#### 学习内容

**1. 为什么选 React？**

```
后端工程师视角：
- React 只是一个 UI 库（不像 Django/Spring 是全栈框架）
- 组件化思想 ≈ 微服务架构（每个组件独立、可复用）
- 单向数据流 ≈ 事件溯源（状态变化 → UI 更新）
- Virtual DOM ≈ 数据库的 WAL（Write-Ahead Log），批量更新
- JSX ≈ 模板引擎（类似 Go template / Jinja2，但在 JS 里写）
```

**2. 创建 React 项目**

```bash
# Vite（推荐，比 CRA 快 10 倍+）
pnpm create vite my-app --template react-ts
cd my-app
pnpm install
pnpm dev

# TypeScript 模板（推荐后端工程师用 TS）
pnpm create vite my-app --template react-ts
```

**3. JSX 本质**

```jsx
// JSX 是语法糖，会被编译成 React.createElement() 调用
// 你写的：
const element = <h1 className="title">Hello, {name}!</h1>;

// 编译后：
const element = React.createElement('h1', { className: 'title' }, 'Hello, ', name, '!');

// 后端类比：JSX ≈ Go template，但更灵活
// Go template: <h1>{{ .Name }}</h1>
// JSX: <h1>{name}</h1>
```

**4. 组件基础**

```jsx
// 函数组件（唯一推荐的方式）
function Greeting({ name, age = 18 }) {
  // props 是只读的！（类似函数参数）
  return (
    <div className="greeting">
      <h1>你好，{name}</h1>
      <p>年龄：{age}</p>
    </div>
  );
}

// 箭头函数写法
const Greeting = ({ name, age = 18 }) => (
  <div className="greeting">
    <h1>你好，{name}</h1>
    <p>年龄：{age}</p>
  </div>
);

// 使用组件
function App() {
  return (
    <div>
      <Greeting name="Alice" age={30} />
      <Greeting name="Bob" />  {/* age 使用默认值 18 */}
    </div>
  );
}

// ★ 条件渲染
function UserCard({ user }) {
  return (
    <div>
      {user ? (
        <p>{user.name}</p>
      ) : (
        <p>加载中...</p>
      )}
      
      {/* 短路 */}
      {user.isAdmin && <button>管理面板</button>}
      
      {/* 三元 */}
      <span>{user.online ? '🟢 在线' : '⚫ 离线'}</span>
    </div>
  );
}

// ★ 列表渲染
function UserList({ users }) {
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>  {/* key 必须有！且稳定唯一 */}
          {user.name} - {user.email}
        </li>
      ))}
    </ul>
  );
}

// ★ 事件处理
function SearchBox() {
  const [query, setQuery] = useState('');
  
  const handleChange = (e) => {
    setQuery(e.target.value);
  };
  
  const handleSubmit = (e) => {
    e.preventDefault(); // 阻止表单默认提交
    console.log('搜索:', query);
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={query}
        onChange={handleChange}
        placeholder="搜索..."
      />
      <button type="submit">搜索</button>
    </form>
  );
}

// 后端类比：
// 组件 ≈ Go 的函数（输入 props，输出 UI）
// 条件渲染 ≈ Go template 的 {{ if }}
// 列表渲染 ≈ Go template 的 {{ range }}
// key ≈ 数据库主键（React 用它来高效更新 DOM）
```

**5. useState（状态管理基础）**

```jsx
import { useState } from 'react';

function Counter() {
  // 状态变量 + 更新函数 + 初始值
  const [count, setCount] = useState(0);
  
  // ★ 状态更新是异步的！
  const handleIncrement = () => {
    setCount(prev => prev + 1); // 用函数形式避免闭包陷阱
  };
  
  // ★ 状态更新会触发重新渲染
  // 类似 Go 中修改了状态变量，然后重新渲染模板
  
  return (
    <div>
      <p>计数：{count}</p>
      <button onClick={handleIncrement}>+1</button>
      <button onClick={() => setCount(count - 1)}>-1</button>
      <button onClick={() => setCount(0)}>重置</button>
    </div>
  );
}

// ★ 对象/数组状态更新（不可变！）
function UserForm() {
  const [form, setForm] = useState({ name: '', email: '', role: 'user' });
  
  const updateField = (field, value) => {
    setForm(prev => ({ ...prev, [field]: value }));
    // 必须创建新对象！不能直接修改 prev
    // 类似 Go 中返回新的 struct 而不是修改原来的
  };
  
  return (
    <input
      value={form.name}
      onChange={e => updateField('name', e.target.value)}
    />
  );
}

// 后端类比：
// useState ≈ Go 中的一个变量 + 变更通知机制
// setCount ≈ 修改变量 + 通知 UI 重新渲染
// 不可变更新 ≈ Go 中值类型的赋值（int, string, struct 都是值拷贝）
```

#### 实战练习

1. **创建一个温度转换器**：摄氏度 ↔ 华氏度，双向绑定
2. **创建一个星级评分组件**：支持半星、只读模式、自定义大小
3. **创建一个标签输入组件**：输入后回车添加标签，点击 × 删除，支持退格删除

---

### Day 14：React 进阶（useEffect、useRef、自定义 Hook）

#### 学习内容

**1. useEffect（副作用处理）**

```jsx
import { useState, useEffect } from 'react';

// ★ 基础用法（每次渲染后执行）
function Timer() {
  const [count, setCount] = useState(0);
  
  useEffect(() => {
    console.log('组件渲染了');
  }); // 没有依赖数组 = 每次渲染都执行（通常不是你想要的）
  
  return <p>{count}</p>;
}

// ★ 空依赖数组（只在挂载时执行一次）
function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  
  useEffect(() => {
    // 组件挂载时执行（类似 Go 的 init 或 Python 的 __init__）
    fetch(`/api/users/${userId}`)
      .then(res => res.json())
      .then(setUser);
  }, []); // 空数组 = 只执行一次
  
  if (!user) return <p>加载中...</p>;
  return <p>{user.name}</p>;
}

// ★ 有依赖（依赖变化时执行）
function SearchResults({ query }) {
  const [results, setResults] = useState([]);
  
  useEffect(() => {
    if (!query) return;
    
    // 防抖搜索
    const timer = setTimeout(() => {
      fetch(`/api/search?q=${query}`)
        .then(res => res.json())
        .then(setResults);
    }, 300);
    
    // ★★★ 清理函数（重要！）
    return () => clearTimeout(timer);
    // 下次 effect 执行前 / 组件卸载时调用
    // 类似 Go 的 defer
  }, [query]); // query 变化时重新执行
  
  return (
    <ul>
      {results.map(r => <li key={r.id}>{r.title}</li>)}
    </ul>
  );
}

// ★ 常见 useEffect 模式

// 1. 订阅/取消订阅
useEffect(() => {
  const ws = new WebSocket('wss://api.example.com');
  ws.onmessage = (e) => handleMessage(JSON.parse(e.data));
  return () => ws.close(); // 清理
}, []);

// 2. 事件监听
useEffect(() => {
  const handler = (e) => { /* ... */ };
  window.addEventListener('resize', handler);
  return () => window.removeEventListener('resize', handler);
}, []);

// 3. 定时器
useEffect(() => {
  const id = setInterval(() => setCount(c => c + 1), 1000);
  return () => clearInterval(id);
}, []);

// 后端类比：
// useEffect(fn, []) ≈ Go 的 init() 函数
// useEffect(fn, [dep]) ≈ Go 中监听 channel，当数据变化时触发
// cleanup ≈ Go 的 defer
```

**2. useRef**

```jsx
import { useRef } from 'react';

// 1. 引用 DOM 元素
function AutoFocusInput() {
  const inputRef = useRef(null);
  
  useEffect(() => {
    inputRef.current.focus(); // 直接操作 DOM
  }, []);
  
  return <input ref={inputRef} placeholder="自动聚焦" />;
}

// 2. 存储不触发渲染的值
function StopWatch() {
  const timerRef = useRef(null);
  const [seconds, setSeconds] = useState(0);
  
  const start = () => {
    timerRef.current = setInterval(() => {
      setSeconds(s => s + 1);
    }, 1000);
  };
  
  const stop = () => clearInterval(timerRef.current);
  
  // ★ useRef vs useState：
  // useRef 修改不触发重新渲染
  // useState 修改触发重新渲染
  // 后端类比：useRef ≈ Go 的全局变量（不通知 UI），useState ≈ 响应式变量
}

// 3. 存储上一个值
function usePrevious(value) {
  const ref = useRef(value);
  useEffect(() => {
    ref.current = value;
  }, [value]);
  return ref.current;
}
```

**3. 自定义 Hook（★★★ React 的核心模式）**

```jsx
// ★ 封装可复用的逻辑
function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(() => {
    const stored = localStorage.getItem(key);
    return stored ? JSON.parse(stored) : initialValue;
  });
  
  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);
  
  return [value, setValue];
}

// 使用
function Settings() {
  const [theme, setTheme] = useLocalStorage('theme', 'light');
  const [lang, setLang] = useLocalStorage('lang', 'zh');
  
  return (
    <select value={theme} onChange={e => setTheme(e.target.value)}>
      <option value="light">亮色</option>
      <option value="dark">暗色</option>
    </select>
  );
}

// ★ 更多实用自定义 Hook

// useFetch — 数据请求
function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  
  useEffect(() => {
    setLoading(true);
    fetch(url)
      .then(res => res.json())
      .then(setData)
      .catch(setError)
      .finally(() => setLoading(false));
  }, [url]);
  
  return { data, loading, error };
}

// useDebounce — 防抖值
function useDebounce(value, delay) {
  const [debounced, setDebounced] = useState(value);
  useEffect(() => {
    const timer = setTimeout(() => setDebounced(value), delay);
    return () => clearTimeout(timer);
  }, [value, delay]);
  return debounced;
}

// useClickOutside — 点击外部
function useClickOutside(ref, handler) {
  useEffect(() => {
    const listener = (e) => {
      if (!ref.current || ref.current.contains(e.target)) return;
      handler(e);
    };
    document.addEventListener('mousedown', listener);
    return () => document.removeEventListener('mousedown', listener);
  }, [ref, handler]);
}

// 后端类比：
// 自定义 Hook ≈ Go 的中间件 / 装饰器模式
// 封装通用逻辑，在多个组件间复用
```

#### 实战练习

1. **实现 `useFetch` Hook**：支持取消请求（AbortController）、缓存、重试
2. **实现 `useInfiniteScroll` Hook**：用 IntersectionObserver 实现无限滚动
3. **实现 `useMediaQuery` Hook**：响应式媒体查询

---

### Day 15：React Router 与状态管理

#### 学习内容

**1. React Router（客户端路由）**

```jsx
import { BrowserRouter, Routes, Route, Link, useNavigate, useParams, useSearchParams } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">首页</Link>
        <Link to="/users">用户</Link>
        <Link to="/about">关于</Link>
      </nav>
      
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/users" element={<UserList />} />
        <Route path="/users/:id" element={<UserDetail />} /> {/* 动态路由 */}
        <Route path="/about" element={<About />} />
        <Route path="*" element={<NotFound />} /> {/* 404 */}
      </Routes>
    </BrowserRouter>
  );
}

// 路由参数
function UserDetail() {
  const { id } = useParams(); // URL 参数 /users/123
  const [searchParams] = useSearchParams(); // 查询参数 ?tab=posts
  const tab = searchParams.get('tab') || 'info';
  const navigate = useNavigate(); // 编程式导航
  
  return (
    <div>
      <h1>用户 {id}</h1>
      <button onClick={() => navigate('/users')}>返回</button>
      <button onClick={() => navigate(-1)}>后退</button>
    </div>
  );
}

// 嵌套路由
function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/dashboard" element={<DashboardLayout />}>
          <Route index element={<Overview />} />
          <Route path="settings" element={<Settings />} />
          <Route path="profile" element={<Profile />} />
        </Route>
      </Routes>
    </BrowserRouter>
  );
}

function DashboardLayout() {
  return (
    <div className="dashboard">
      <aside>
        <Link to="/dashboard">概览</Link>
        <Link to="/dashboard/settings">设置</Link>
        <Link to="/dashboard/profile">资料</Link>
      </aside>
      <main>
        <Outlet /> {/* 子路由渲染位置 */}
      </main>
    </div>
  );
}

// 路由守卫（类似后端中间件）
function RequireAuth({ children }) {
  const token = localStorage.getItem('token');
  if (!token) {
    return <Navigate to="/login" replace />;
  }
  return children;
}

// 使用
<Route path="/admin" element={
  <RequireAuth>
    <AdminPanel />
  </RequireAuth>
} />

// 后端类比：
// React Router ≈ Go 的 http.ServeMux / chi router
// <Route> ≈ mux.HandleFunc
// useParams ≈ 从 URL path 提取参数
// useSearchParams ≈ 从 query string 提取参数
// Navigate ≈ http.Redirect
// 路由守卫 ≈ 认证中间件
```

**2. 状态管理（Context API + Zustand）**

```jsx
// === 方案1：Context API（适合小型应用）===
import { createContext, useContext, useReducer } from 'react';

// 创建 Context
const AuthContext = createContext(null);

// Provider 组件
function AuthProvider({ children }) {
  const [state, dispatch] = useReducer(authReducer, initialState);
  
  return (
    <AuthContext.Provider value={{ ...state, dispatch }}>
      {children}
    </AuthContext.Provider>
  );
}

// Reducer（类似 Redux 的 reducer，类似 Go 的状态机）
function authReducer(state, action) {
  switch (action.type) {
    case 'LOGIN':
      return { ...state, user: action.payload, isAuthenticated: true };
    case 'LOGOUT':
      return { ...state, user: null, isAuthenticated: false };
    default:
      return state;
  }
}

// 自定义 Hook 使用 Context
function useAuth() {
  const context = useContext(AuthContext);
  if (!context) throw new Error('useAuth must be used within AuthProvider');
  return context;
}

// 在组件中使用
function Navbar() {
  const { user, dispatch } = useAuth();
  
  return user ? (
    <span>欢迎，{user.name}</span>
  ) : (
    <button onClick={() => dispatch({ type: 'LOGIN', payload: { name: 'Alice' } })}>
      登录
    </button>
  );
}

// === 方案2：Zustand（推荐！比 Redux 简单 10 倍）===
import { create } from 'zustand';

const useStore = create((set, get) => ({
  // 状态
  user: null,
  token: null,
  
  // 操作
  login: (userData, token) => set({ user: userData, token }),
  logout: () => set({ user: null, token: null }),
  
  // 派生状态
  isAdmin: () => get().user?.role === 'admin',
}));

// 使用
function Profile() {
  const { user, logout } = useStore();
  const isAdmin = useStore(s => s.isAdmin());
  
  return (
    <div>
      <p>{user.name}</p>
      {isAdmin && <button>管理面板</button>}
      <button onClick={logout}>退出</button>
    </div>
  );
}

// 后端类比：
// Context ≈ Go 的 context.Context（传递请求级别的值）
// useReducer ≈ Go 的状态机模式
// Zustand ≈ 一个全局的内存数据库 + CRUD 操作
```

#### 实战练习

1. **实现一个带路由的 SPA**：首页、用户列表、用户详情、登录页，带路由守卫
2. **用 Zustand 实现购物车**：添加/删除商品、修改数量、计算总价、持久化到 localStorage

---

### Day 16：Vue 3 核心概念（快速了解）

> **建议**：主攻 React，但了解 Vue 3 的核心概念，拓宽视野

```vue
<!-- Vue 3 组合式 API（Composition API） -->
<script setup>
import { ref, reactive, computed, watch, onMounted } from 'vue'

// ref — 基本类型响应式（类似 React 的 useState）
const count = ref(0)
const name = ref('Alice')

// reactive — 对象响应式
const user = reactive({
  name: 'Alice',
  age: 30,
  hobbies: ['coding', 'reading'],
})

// computed — 计算属性（有缓存）
const doubleCount = computed(() => count.value * 2)
const fullName = computed(() => `${user.name}, ${user.age}岁`)

// watch — 侦听器
watch(count, (newVal, oldVal) => {
  console.log(`count: ${oldVal} → ${newVal}`)
})

watch(() => user.name, (newName) => {
  console.log('名字变了:', newName)
})

// 生命周期
onMounted(() => {
  console.log('组件挂载了')
})

// 方法
function increment() {
  count.value++ // 注意要 .value！
}
</script>

<template>
  <!-- 模板语法 -->
  <div>
    <p>{{ name }}</p>
    <p>计数：{{ count }}（双倍：{{ doubleCount }}）</p>
    <button @click="increment">+1</button>
    
    <!-- v-if 条件渲染 -->
    <p v-if="count > 10">大于10</p>
    <p v-else-if="count > 5">大于5</p>
    <p v-else>小于等于5</p>
    
    <!-- v-for 列表渲染 -->
    <ul>
      <li v-for="hobby in user.hobbies" :key="hobby">
        {{ hobby }}
      </li>
    </ul>
    
    <!-- v-model 双向绑定（React 没有这个！） -->
    <input v-model="name" placeholder="输入名字">
    
    <!-- v-show（display:none，不销毁 DOM） -->
    <div v-show="count > 0">可见</div>
  </div>
</template>

<style scoped>
/* scoped 样式只作用于当前组件 */
p { color: #333; }
</style>
```

**React vs Vue 对比（后端工程师视角）**

| 特性 | React | Vue |
|------|-------|-----|
| 模板 | JSX（JS 中写 HTML） | Template（HTML 中写 JS） |
| 状态 | useState | ref / reactive |
| 副作用 | useEffect | watch / onMounted |
| 计算属性 | useMemo | computed |
| 双向绑定 | 手动（value + onChange） | v-model（内置） |
| 生态 | 更大、更灵活 | 更统一、更易上手 |
| TypeScript | 原生支持 | 良好支持 |
| 学习曲线 | 较陡（JSX + Hooks 概念多） | 较缓（模板更直观） |

---

### Day 17：前端工程化（Vite、ESLint、TypeScript）

#### 学习内容

**1. Vite（构建工具）**

```bash
# 创建项目
pnpm create vite my-app --template react-ts

# 开发
pnpm dev          # 启动开发服务器（秒启动！）
pnpm build        # 生产构建
pnpm preview      # 预览构建结果

# 添加依赖
pnpm add axios zustand react-router-dom
pnpm add -D @types/node  # 开发依赖
```

```javascript
// vite.config.ts
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import path from 'path'

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'), // 路径别名
    },
  },
  server: {
    port: 3000,
    proxy: {
      '/api': {
        target: 'http://localhost:8080', // 代理后端 API
        changeOrigin: true,
      },
    },
  },
})
```

**2. TypeScript 基础（后端工程师会很快上手）**

```typescript
// 基础类型（和 Go 类似）
let name: string = 'Alice';
let age: number = 30;
let isActive: boolean = true;
let items: string[] = ['a', 'b', 'c'];
let tuple: [string, number] = ['Alice', 30];

// 接口（类似 Go 的 struct 定义）
interface User {
  id: number;
  name: string;
  email: string;
  age?: number;           // 可选属性
  readonly createdAt: Date; // 只读
}

// 类型别名
type Status = 'active' | 'inactive' | 'banned'; // 联合类型
type ID = string | number;

// 泛型（和 Go 的泛型类似）
function getFirst<T>(arr: T[]): T | undefined {
  return arr[0];
}
getFirst<number>([1, 2, 3]); // 1
getFirst(['a', 'b']);        // 'a'（自动推断）

interface ApiResponse<T> {
  code: number;
  message: string;
  data: T;
}

type UserResponse = ApiResponse<User>;
type UserListResponse = ApiResponse<User[]>;

// React + TypeScript
interface ButtonProps {
  label: string;
  onClick: () => void;
  variant?: 'primary' | 'secondary';
  disabled?: boolean;
  children?: React.ReactNode;
}

function Button({ label, onClick, variant = 'primary', disabled }: ButtonProps) {
  return (
    <button onClick={onClick} disabled={disabled} className={variant}>
      {label}
    </button>
  );
}

// 后端类比：
// TypeScript ≈ Go 的类型系统（但更灵活）
// interface ≈ Go 的 struct
// type ≈ Go 的 type alias
// 泛型 ≈ Go 1.18+ 的泛型
// ?可选 ≈ Go 的指针类型（nil 表示没有值）
```

**3. ESLint + Prettier**

```bash
# 安装
pnpm add -D eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin prettier eslint-config-prettier

# eslint.config.js
export default [
  {
    files: ['src/**/*.{ts,tsx}'],
    rules: {
      'no-unused-vars': 'warn',
      'no-console': ['warn', { allow: ['warn', 'error'] }],
      '@typescript-eslint/no-explicit-any': 'warn',
    },
  },
];
```

**4. 目录结构（推荐）**

```
src/
├── assets/          # 静态资源（图片、字体）
├── components/      # 通用组件
│   ├── ui/          # 基础 UI 组件（Button, Input, Modal）
│   └── layout/      # 布局组件（Header, Sidebar, Footer）
├── hooks/           # 自定义 Hooks
├── pages/           # 页面组件（路由级别）
├── services/        # API 请求
├── stores/          # 状态管理
├── types/           # TypeScript 类型定义
├── utils/           # 工具函数
├── styles/          # 全局样式
├── App.tsx          # 根组件
└── main.tsx         # 入口文件
```

#### 实战练习

1. **用 TypeScript 重写第二周的 TODO 应用**：定义完整的类型接口
2. **配置 ESLint + Prettier**：统一代码风格
3. **配置路径别名**：用 `@/components/Button` 代替 `../../../components/Button`

---

### Day 18：CSS 工具与组件库 + 第三周项目

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

---

## 第四周：进阶实战与全栈打通

> **本周目标**：掌握性能优化、测试、部署、全栈开发，完成一个完整的全栈项目

---

### Day 19：性能优化

#### 学习内容

**1. 渲染性能**

```jsx
// ★ React.memo — 避免不必要的重新渲染
const ExpensiveList = React.memo(function ExpensiveList({ items }) {
  return items.map(item => <ListItem key={item.id} item={item} />);
});

// ★ useMemo — 缓存计算结果
function UserDashboard({ users, filter }) {
  const filteredUsers = useMemo(() => {
    return users.filter(u => u.name.includes(filter));
  }, [users, filter]); // 只有 users 或 filter 变化时重新计算
  
  return <UserList users={filteredUsers} />;
}

// ★ useCallback — 缓存函数引用
function Parent() {
  const [count, setCount] = useState(0);
  
  const handleClick = useCallback(() => {
    console.log('clicked');
  }, []); // 空依赖 = 函数永远不会变
  
  return <Child onClick={handleClick} />;
}

// 后端类比：
// React.memo ≈ Go 的 sync.Pool（复用对象，减少分配）
// useMemo ≈ Go 的缓存（避免重复计算）
// useCallback ≈ Go 中缓存函数引用
```

**2. 代码分割与懒加载**

```jsx
import { lazy, Suspense } from 'react';

// 路由级懒加载（最常用）
const Home = lazy(() => import('./pages/Home'));
const Admin = lazy(() => import('./pages/Admin'));

function App() {
  return (
    <Suspense fallback={<Loading />}>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/admin" element={<Admin />} />
      </Routes>
    </Suspense>
  );
}

// 组件级懒加载
const HeavyChart = lazy(() => import('./components/HeavyChart'));

function Dashboard() {
  const [showChart, setShowChart] = useState(false);
  
  return (
    <div>
      <button onClick={() => setShowChart(true)}>显示图表</button>
      {showChart && (
        <Suspense fallback={<div>加载图表中...</div>}>
          <HeavyChart />
        </Suspense>
      )}
    </div>
  );
}

// 后端类比：
// 代码分割 ≈ Go 的 plugin 模式（按需加载）
// 懒加载 ≈ Go 的延迟初始化（sync.Once）
```

**3. 关键性能指标（Core Web Vitals）**

```
LCP (Largest Contentful Paint) — 最大内容绘制 < 2.5s
FID (First Input Delay) — 首次输入延迟 < 100ms
CLS (Cumulative Layout Shift) — 累积布局偏移 < 0.1
INP (Interaction to Next Paint) — 交互到下次绘制 < 200ms

优化手段：
- 图片优化：WebP 格式、懒加载、响应式图片、CDN
- 代码分割：路由懒加载、动态 import
- 缓存策略：Service Worker、HTTP 缓存头
- 渲染优化：虚拟列表、防抖节流、避免强制同步布局
- 资源优化：Tree Shaking、压缩、预加载
```

**4. 虚拟列表（Virtual List）**

```jsx
// 当列表有上千条数据时，只渲染可视区域的元素
import { useVirtualizer } from '@tanstack/react-virtual';

function VirtualList({ items }) {
  const parentRef = useRef(null);
  
  const virtualizer = useVirtualizer({
    count: items.length,
    getScrollElement: () => parentRef.current,
    estimateSize: () => 50, // 每项高度
    overscan: 5, // 额外渲染 5 项
  });
  
  return (
    <div ref={parentRef} style={{ height: '600px', overflow: 'auto' }}>
      <div style={{ height: `${virtualizer.getTotalSize()}px` }}>
        {virtualizer.getVirtualItems().map(virtualItem => (
          <div
            key={virtualItem.key}
            style={{
              position: 'absolute',
              top: 0,
              transform: `translateY(${virtualItem.start}px)`,
              height: `${virtualItem.size}px`,
            }}
          >
            {items[virtualItem.index].name}
          </div>
        ))}
      </div>
    </div>
  );
}
```

#### 实战练习

1. **用 React DevTools Profiler 分析组件渲染性能**：找出不必要的重新渲染
2. **实现一个虚拟滚动列表**：渲染 10000 条数据，保持 60fps
3. **用 Lighthouse 审计你的博客项目**：优化到 90+ 分

---

### Day 20：前端测试

#### 学习内容

```bash
# 安装测试工具
pnpm add -D vitest @testing-library/react @testing-library/jest-dom @testing-library/user-event jsdom
```

**1. 单元测试**

```typescript
// utils.test.ts
import { describe, it, expect } from 'vitest';
import { formatCurrency, validateEmail, debounce } from './utils';

describe('formatCurrency', () => {
  it('应该正确格式化金额', () => {
    expect(formatCurrency(1234.5)).toBe('¥1,234.50');
    expect(formatCurrency(0)).toBe('¥0.00');
    expect(formatCurrency(-100)).toBe('-¥100.00');
  });
});

describe('validateEmail', () => {
  it('应该验证有效邮箱', () => {
    expect(validateEmail('test@example.com')).toBe(true);
    expect(validateEmail('invalid')).toBe(false);
    expect(validateEmail('')).toBe(false);
  });
});
```

**2. 组件测试**

```tsx
// Counter.test.tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { describe, it, expect } from 'vitest';
import Counter from './Counter';

describe('Counter', () => {
  it('应该正确渲染初始值', () => {
    render(<Counter initialCount={5} />);
    expect(screen.getByText('5')).toBeInTheDocument();
  });
  
  it('点击 +1 按钮应该增加计数', async () => {
    render(<Counter initialCount={0} />);
    const button = screen.getByRole('button', { name: /increment/i });
    fireEvent.click(button);
    expect(screen.getByText('1')).toBeInTheDocument();
  });
  
  it('应该调用 onChange 回调', async () => {
    const handleChange = vi.fn();
    render(<Counter initialCount={0} onChange={handleChange} />);
    fireEvent.click(screen.getByRole('button', { name: /increment/i }));
    expect(handleChange).toHaveBeenCalledWith(1);
  });
});
```

**3. E2E 测试（Playwright）**

```bash
pnpm add -D @playwright/test
npx playwright install
```

```typescript
// tests/login.spec.ts
import { test, expect } from '@playwright/test';

test('用户登录流程', async ({ page }) => {
  await page.goto('/login');
  
  await page.fill('[name="email"]', 'test@example.com');
  await page.fill('[name="password"]', 'password123');
  await page.click('button[type="submit"]');
  
  await expect(page).toHaveURL('/dashboard');
  await expect(page.getByText('欢迎')).toBeVisible();
});
```

**测试策略（后端工程师视角）**

| 测试类型 | 类比 | 工具 | 覆盖范围 |
|----------|------|------|----------|
| 单元测试 | Go 的 `go test` | Vitest | 工具函数、纯逻辑 |
| 组件测试 | Go 的 handler 测试 | Testing Library | 组件交互 |
| E2E 测试 | Go 的集成测试 | Playwright | 完整用户流程 |

---

### Day 21：Next.js 与服务端渲染（SSR）

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

---

### Day 22：全栈开发（前后端联调）

#### 学习内容

**1. 前后端通信最佳实践**

```typescript
// services/api.ts — 统一的 API 客户端
const BASE_URL = '/api';

class ApiClient {
  private baseUrl: string;
  
  constructor(baseUrl: string) {
    this.baseUrl = baseUrl;
  }
  
  private async request<T>(
    endpoint: string,
    options: RequestInit = {}
  ): Promise<T> {
    const url = `${this.baseUrl}${endpoint}`;
    const token = localStorage.getItem('token');
    
    const response = await fetch(url, {
      ...options,
      headers: {
        'Content-Type': 'application/json',
        ...(token ? { Authorization: `Bearer ${token}` } : {}),
        ...options.headers,
      },
    });
    
    if (!response.ok) {
      const error = await response.json().catch(() => ({}));
      throw new ApiError(response.status, error.message || '请求失败');
    }
    
    return response.json();
  }
  
  get<T>(endpoint: string) {
    return this.request<T>(endpoint);
  }
  
  post<T>(endpoint: string, data: unknown) {
    return this.request<T>(endpoint, {
      method: 'POST',
      body: JSON.stringify(data),
    });
  }
  
  put<T>(endpoint: string, data: unknown) {
    return this.request<T>(endpoint, {
      method: 'PUT',
      body: JSON.stringify(data),
    });
  }
  
  delete<T>(endpoint: string) {
    return this.request<T>(endpoint, { method: 'DELETE' });
  }
}

class ApiError extends Error {
  constructor(public status: number, message: string) {
    super(message);
  }
}

export const api = new ApiClient(BASE_URL);

// 使用
const users = await api.get<User[]>('/users');
const newUser = await api.post<User>('/users', { name: 'Alice' });
await api.delete(`/users/${id}`);
```

**2. 跨域处理（CORS）**

```go
// Go 后端设置 CORS（后端工程师应该很熟悉）
// 使用 gin 框架
import "github.com/gin-contrib/cors"

r.Use(cors.New(cors.Config{
    AllowOrigins:     []string{"http://localhost:3000"},
    AllowMethods:     []string{"GET", "POST", "PUT", "DELETE", "OPTIONS"},
    AllowHeaders:     []string{"Origin", "Content-Type", "Authorization"},
    AllowCredentials: true,
    MaxAge:           12 * time.Hour,
}))
```

**3. JWT 认证**

```typescript
// 前端 Token 管理
function setToken(token: string) {
  localStorage.setItem('token', token);
}

function getToken(): string | null {
  return localStorage.getItem('token');
}

function clearToken() {
  localStorage.removeItem('token');
}

// 自动刷新 Token
let refreshTimer: NodeJS.Timeout;

function setupTokenRefresh() {
  refreshTimer = setInterval(async () => {
    try {
      const newToken = await api.post('/auth/refresh', {});
      setToken(newToken.token);
    } catch {
      clearToken();
      window.location.href = '/login';
    }
  }, 15 * 60 * 1000); // 每 15 分钟刷新
}

// 请求拦截器（自动添加 Token）
const originalFetch = window.fetch;
window.fetch = async (url, options) => {
  const token = getToken();
  if (token) {
    options = {
      ...options,
      headers: {
        ...options.headers,
        Authorization: `Bearer ${token}`,
      },
    };
  }
  return originalFetch(url, options);
};
```

**4. WebSocket 实时通信**

```typescript
// WebSocket Hook
function useWebSocket(url: string) {
  const [messages, setMessages] = useState<Message[]>([]);
  const wsRef = useRef<WebSocket | null>(null);
  
  useEffect(() => {
    const ws = new WebSocket(url);
    wsRef.current = ws;
    
    ws.onmessage = (event) => {
      const msg = JSON.parse(event.data);
      setMessages(prev => [...prev, msg]);
    };
    
    ws.onclose = () => {
      // 自动重连
      setTimeout(() => reconnect(), 3000);
    };
    
    return () => ws.close();
  }, [url]);
  
  const send = (data: unknown) => {
    wsRef.current?.send(JSON.stringify(data));
  };
  
  return { messages, send };
}
```

---

### Day 23：部署与 DevOps

#### 学习内容

**1. Vercel 部署（最简单）**

```bash
# 安装 Vercel CLI
pnpm add -g vercel

# 部署
vercel

# 生产部署
vercel --prod

# 环境变量
vercel env add NEXT_PUBLIC_API_URL
```

**2. Docker 部署**

```dockerfile
# 多阶段构建
# 构建阶段
FROM node:20-alpine AS builder
WORKDIR /app
COPY package.json pnpm-lock.yaml ./
RUN corepack enable && pnpm install --frozen-lockfile
COPY . .
RUN pnpm build

# 运行阶段
FROM node:20-alpine AS runner
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package.json ./

EXPOSE 3000
ENV NODE_ENV=production
CMD ["node", "dist/server.js"]

# 后端工程师应该很熟悉 Docker！
# 前端部署和后端差不多，只是最终产物是静态文件
```

**3. Nginx 配置（静态文件服务）**

```nginx
server {
    listen 80;
    server_name example.com;
    root /usr/share/nginx/html;
    index index.html;
    
    # SPA 路由 — 所有路由都返回 index.html
    location / {
        try_files $uri $uri/ /index.html;
    }
    
    # API 反向代理
    location /api/ {
        proxy_pass http://backend:8080/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
    
    # 静态资源缓存
    location /assets/ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }
    
    # Gzip 压缩
    gzip on;
    gzip_types text/plain text/css application/json application/javascript text/xml;
}
```

**4. CI/CD（GitHub Actions）**

```yaml
# .github/workflows/deploy.yml
name: Deploy
on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: pnpm/action-setup@v2
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: 'pnpm'
      - run: pnpm install --frozen-lockfile
      - run: pnpm lint
      - run: pnpm test
      - run: pnpm build

  deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: amondnet/vercel-action@v25
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-org-id: ${{ secrets.VERCEL_ORG_ID }}
          vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID }}
          vercel-args: '--prod'
```

---

### Day 24：第四周项目 — 全栈全功能项目

#### 项目：实时协作任务管理平台

**功能清单**：

```
用户系统：
□ 注册/登录（JWT 认证）
□ 个人资料编辑
□ 头像上传

项目管理：
□ 创建/编辑/删除项目
□ 项目成员管理（邀请/移除）
□ 项目设置

任务管理：
□ 看板视图（拖拽排序）
□ 列表视图
□ 日历视图
□ 任务创建/编辑/删除
□ 任务分配、优先级、截止日期
□ 任务评论
□ 任务附件上传

实时功能：
□ WebSocket 实时通知
□ 在线用户显示
□ 实时任务状态更新

其他：
□ 全局搜索
□ 暗色模式
□ 响应式设计
□ 键盘快捷键
□ 拖拽上传
```

**技术栈**：

| 层 | 技术 |
|----|------|
| 前端框架 | React + TypeScript |
| 构建工具 | Vite |
| 状态管理 | Zustand |
| 路由 | React Router |
| UI | Tailwind CSS + shadcn/ui |
| 拖拽 | dnd-kit |
| 请求 | Axios + React Query |
| 实时 | WebSocket |
| 测试 | Vitest + Playwright |
| 后端 | 你的 Golang/Python 后端 |
| 部署 | Vercel + Docker |

---

## 附录：学习资源汇总

### 必读文档（按优先级）

| 资源 | 说明 | 优先级 |
|------|------|--------|
| [MDN Web Docs](https://developer.mozilla.org/) | 前端权威文档 | ★★★★★ |
| [React 官方文档](https://react.dev/) | React 新版文档（超好） | ★★★★★ |
| [TypeScript Handbook](https://www.typescriptlang.org/docs/) | TS 官方手册 | ★★★★ |
| [Tailwind CSS 文档](https://tailwindcss.com/docs) | Tailwind 用法 | ★★★★ |
| [web.dev](https://web.dev/) | Google 性能最佳实践 | ★★★ |
| [JavaScript.info](https://javascript.info/) | JS 深入教程 | ★★★ |

### 推荐视频/课程

| 资源 | 说明 |
|------|------|
| Fireship（YouTube） | 2 分钟速成系列，后端工程师最爱 |
| Theo - t3.gg（YouTube） | 前端工程化深度内容 |
| Kent C. Dodds（YouTube） | React 测试权威 |
| Frontend Masters | 系统课程（付费） |
| EpicWeb.dev | 全栈 React 课程（付费） |

### 练手项目推荐

1. **个人博客**（SSR/SSG）— 学习 Next.js
2. **实时聊天应用**（WebSocket）— 学习实时通信
3. **电商后台管理**（CRUD + 图表）— 学习企业级开发
4. **Markdown 编辑器**（富文本）— 学习复杂交互
5. **CLI 工具**（Node.js）— 结合后端经验
6. **浏览器扩展**（Chrome Extension）— 了解浏览器 API

### 每日学习节奏建议

```
上午（2-3 小时）：
  学习新概念 + 阅读文档
  边看边写代码验证

下午（2-3 小时）：
  实战练习 / 项目开发
  遇到问题查文档 / Google

晚上（30 分钟）：
  复习当天内容
  写学习笔记
  看一篇前端相关文章
```

---

> **最后的话**：作为后端工程师，你的优势在于理解数据流、API 设计、系统架构。前端的核心难点在于**状态管理**和**用户体验**。不要试图记住所有 API，而是理解核心概念，需要时查文档即可。前端技术更新快，但底层原理不变。掌握原理，你就有了快速学习任何新框架的能力。加油！🚀
