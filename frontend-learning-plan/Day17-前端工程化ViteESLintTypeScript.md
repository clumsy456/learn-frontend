# Day 17：前端工程化（Vite、ESLint、TypeScript）

#### 学习内容

**1. Vite（构建工具）**

```bash
# 创建项目
pnpm create vite my-app --template react-ts

# 开发
pnpm dev          # 启动开发服务器（秒启动！）
pnpm build        # 生产构建
pnpm preview      # 预览构建结果

# 添加依赖
pnpm add axios zustand react-router-dom
pnpm add -D @types/node  # 开发依赖
```

```javascript
// vite.config.ts
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import path from 'path'

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'), // 路径别名
    },
  },
  server: {
    port: 3000,
    proxy: {
      '/api': {
        target: 'http://localhost:8080', // 代理后端 API
        changeOrigin: true,
      },
    },
  },
})
```

**2. TypeScript 基础（后端工程师会很快上手）**

```typescript
// 基础类型（和 Go 类似）
let name: string = 'Alice';
let age: number = 30;
let isActive: boolean = true;
let items: string[] = ['a', 'b', 'c'];
let tuple: [string, number] = ['Alice', 30];

// 接口（类似 Go 的 struct 定义）
interface User {
  id: number;
  name: string;
  email: string;
  age?: number;           // 可选属性
  readonly createdAt: Date; // 只读
}

// 类型别名
type Status = 'active' | 'inactive' | 'banned'; // 联合类型
type ID = string | number;

// 泛型（和 Go 的泛型类似）
function getFirst<T>(arr: T[]): T | undefined {
  return arr[0];
}
getFirst<number>([1, 2, 3]); // 1
getFirst(['a', 'b']);        // 'a'（自动推断）

interface ApiResponse<T> {
  code: number;
  message: string;
  data: T;
}

type UserResponse = ApiResponse<User>;
type UserListResponse = ApiResponse<User[]>;

// React + TypeScript
interface ButtonProps {
  label: string;
  onClick: () => void;
  variant?: 'primary' | 'secondary';
  disabled?: boolean;
  children?: React.ReactNode;
}

function Button({ label, onClick, variant = 'primary', disabled }: ButtonProps) {
  return (
    <button onClick={onClick} disabled={disabled} className={variant}>
      {label}
    </button>
  );
}

// 后端类比：
// TypeScript ≈ Go 的类型系统（但更灵活）
// interface ≈ Go 的 struct
// type ≈ Go 的 type alias
// 泛型 ≈ Go 1.18+ 的泛型
// ?可选 ≈ Go 的指针类型（nil 表示没有值）
```

**3. ESLint + Prettier**

```bash
# 安装
pnpm add -D eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin prettier eslint-config-prettier

# eslint.config.js
export default [
  {
    files: ['src/**/*.{ts,tsx}'],
    rules: {
      'no-unused-vars': 'warn',
      'no-console': ['warn', { allow: ['warn', 'error'] }],
      '@typescript-eslint/no-explicit-any': 'warn',
    },
  },
];
```

**4. 目录结构（推荐）**

```
src/
├── assets/          # 静态资源（图片、字体）
├── components/      # 通用组件
│   ├── ui/          # 基础 UI 组件（Button, Input, Modal）
│   └── layout/      # 布局组件（Header, Sidebar, Footer）
├── hooks/           # 自定义 Hooks
├── pages/           # 页面组件（路由级别）
├── services/        # API 请求
├── stores/          # 状态管理
├── types/           # TypeScript 类型定义
├── utils/           # 工具函数
├── styles/          # 全局样式
├── App.tsx          # 根组件
└── main.tsx         # 入口文件
```

#### 实战练习

1. **用 TypeScript 重写第二周的 TODO 应用**：定义完整的类型接口
2. **配置 ESLint + Prettier**：统一代码风格
3. **配置路径别名**：用 `@/components/Button` 代替 `../../../components/Button`

---
