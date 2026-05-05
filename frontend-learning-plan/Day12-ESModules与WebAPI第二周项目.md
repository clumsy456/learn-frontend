# Day 12：ES Modules 与 Web API + 第二周项目

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
