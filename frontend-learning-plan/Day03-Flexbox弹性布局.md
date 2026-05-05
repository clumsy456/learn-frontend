# Day 3：Flexbox 弹性布局

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
