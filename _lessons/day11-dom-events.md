---
layout: default
title: "Day 11：DOM 操作与事件系统"
categories: ['JavaScript', '第二周']
tags: ['javascript', 'dom', '事件']
---

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
