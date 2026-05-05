# Day 24：第四周项目 — 全栈全功能项目

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
