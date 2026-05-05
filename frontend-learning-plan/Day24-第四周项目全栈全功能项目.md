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
