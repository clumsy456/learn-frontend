---
layout: default
title: "Day 15：React Router 与状态管理"
categories: ['框架', '工程化', '第三周']
tags: ['react', 'router', '状态管理']
---

#### 学习内容

**1. React Router（客户端路由）**

```jsx
import { BrowserRouter, Routes, Route, Link, useNavigate, useParams, useSearchParams } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">首页</Link>
        <Link to="/users">用户</Link>
        <Link to="/about">关于</Link>
      </nav>
      
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/users" element={<UserList />} />
        <Route path="/users/:id" element={<UserDetail />} /> {/* 动态路由 */}
        <Route path="/about" element={<About />} />
        <Route path="*" element={<NotFound />} /> {/* 404 */}
      </Routes>
    </BrowserRouter>
  );
}

// 路由参数
function UserDetail() {
  const { id } = useParams(); // URL 参数 /users/123
  const [searchParams] = useSearchParams(); // 查询参数 ?tab=posts
  const tab = searchParams.get('tab') || 'info';
  const navigate = useNavigate(); // 编程式导航
  
  return (
    <div>
      <h1>用户 {id}</h1>
      <button onClick={() => navigate('/users')}>返回</button>
      <button onClick={() => navigate(-1)}>后退</button>
    </div>
  );
}

// 嵌套路由
function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/dashboard" element={<DashboardLayout />}>
          <Route index element={<Overview />} />
          <Route path="settings" element={<Settings />} />
          <Route path="profile" element={<Profile />} />
        </Route>
      </Routes>
    </BrowserRouter>
  );
}

function DashboardLayout() {
  return (
    <div className="dashboard">
      <aside>
        <Link to="/dashboard">概览</Link>
        <Link to="/dashboard/settings">设置</Link>
        <Link to="/dashboard/profile">资料</Link>
      </aside>
      <main>
        <Outlet /> {/* 子路由渲染位置 */}
      </main>
    </div>
  );
}

// 路由守卫（类似后端中间件）
function RequireAuth({ children }) {
  const token = localStorage.getItem('token');
  if (!token) {
    return <Navigate to="/login" replace />;
  }
  return children;
}

// 使用
<Route path="/admin" element={
  <RequireAuth>
    <AdminPanel />
  </RequireAuth>
} />

// 后端类比：
// React Router ≈ Go 的 http.ServeMux / chi router
// <Route> ≈ mux.HandleFunc
// useParams ≈ 从 URL path 提取参数
// useSearchParams ≈ 从 query string 提取参数
// Navigate ≈ http.Redirect
// 路由守卫 ≈ 认证中间件
```

**2. 状态管理（Context API + Zustand）**

```jsx
// === 方案1：Context API（适合小型应用）===
import { createContext, useContext, useReducer } from 'react';

// 创建 Context
const AuthContext = createContext(null);

// Provider 组件
function AuthProvider({ children }) {
  const [state, dispatch] = useReducer(authReducer, initialState);
  
  return (
    <AuthContext.Provider value={{ ...state, dispatch }}>
      {children}
    </AuthContext.Provider>
  );
}

// Reducer（类似 Redux 的 reducer，类似 Go 的状态机）
function authReducer(state, action) {
  switch (action.type) {
    case 'LOGIN':
      return { ...state, user: action.payload, isAuthenticated: true };
    case 'LOGOUT':
      return { ...state, user: null, isAuthenticated: false };
    default:
      return state;
  }
}

// 自定义 Hook 使用 Context
function useAuth() {
  const context = useContext(AuthContext);
  if (!context) throw new Error('useAuth must be used within AuthProvider');
  return context;
}

// 在组件中使用
function Navbar() {
  const { user, dispatch } = useAuth();
  
  return user ? (
    <span>欢迎，{user.name}</span>
  ) : (
    <button onClick={() => dispatch({ type: 'LOGIN', payload: { name: 'Alice' } })}>
      登录
    </button>
  );
}

// === 方案2：Zustand（推荐！比 Redux 简单 10 倍）===
import { create } from 'zustand';

const useStore = create((set, get) => ({
  // 状态
  user: null,
  token: null,
  
  // 操作
  login: (userData, token) => set({ user: userData, token }),
  logout: () => set({ user: null, token: null }),
  
  // 派生状态
  isAdmin: () => get().user?.role === 'admin',
}));

// 使用
function Profile() {
  const { user, logout } = useStore();
  const isAdmin = useStore(s => s.isAdmin());
  
  return (
    <div>
      <p>{user.name}</p>
      {isAdmin && <button>管理面板</button>}
      <button onClick={logout}>退出</button>
    </div>
  );
}

// 后端类比：
// Context ≈ Go 的 context.Context（传递请求级别的值）
// useReducer ≈ Go 的状态机模式
// Zustand ≈ 一个全局的内存数据库 + CRUD 操作
```

#### 实战练习

1. **实现一个带路由的 SPA**：首页、用户列表、用户详情、登录页，带路由守卫
2. **用 Zustand 实现购物车**：添加/删除商品、修改数量、计算总价、持久化到 localStorage
