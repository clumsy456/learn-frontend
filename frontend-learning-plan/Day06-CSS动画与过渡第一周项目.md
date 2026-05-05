# Day 6：CSS 动画与过渡 + 第一周项目

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
