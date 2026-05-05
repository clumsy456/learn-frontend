---
layout: default
title: "Day 2：CSS 选择器与盒模型"
categories: ['HTML', 'CSS', '第一周']
tags: ['css', '选择器', '盒模型']
---

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
