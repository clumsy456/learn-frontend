# Day 5：响应式设计与移动端适配

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
