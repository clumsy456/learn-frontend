# Day 4：CSS Grid 网格布局

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
