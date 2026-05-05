# Day 1：HTML5 语义化与文档结构

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
