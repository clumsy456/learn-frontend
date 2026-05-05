# Day 13：React 核心概念与 JSX

#### 学习内容

**1. 为什么选 React？**

```
后端工程师视角：
- React 只是一个 UI 库（不像 Django/Spring 是全栈框架）
- 组件化思想 ≈ 微服务架构（每个组件独立、可复用）
- 单向数据流 ≈ 事件溯源（状态变化 → UI 更新）
- Virtual DOM ≈ 数据库的 WAL（Write-Ahead Log），批量更新
- JSX ≈ 模板引擎（类似 Go template / Jinja2，但在 JS 里写）
```

**2. 创建 React 项目**

```bash
# Vite（推荐，比 CRA 快 10 倍+）
pnpm create vite my-app --template react-ts
cd my-app
pnpm install
pnpm dev

# TypeScript 模板（推荐后端工程师用 TS）
pnpm create vite my-app --template react-ts
```

**3. JSX 本质**

```jsx
// JSX 是语法糖，会被编译成 React.createElement() 调用
// 你写的：
const element = <h1 className="title">Hello, {name}!</h1>;

// 编译后：
const element = React.createElement('h1', { className: 'title' }, 'Hello, ', name, '!');

// 后端类比：JSX ≈ Go template，但更灵活
// Go template: <h1>{{ .Name }}</h1>
// JSX: <h1>{name}</h1>
```

**4. 组件基础**

```jsx
// 函数组件（唯一推荐的方式）
function Greeting({ name, age = 18 }) {
  // props 是只读的！（类似函数参数）
  return (
    <div className="greeting">
      <h1>你好，{name}</h1>
      <p>年龄：{age}</p>
    </div>
  );
}

// 箭头函数写法
const Greeting = ({ name, age = 18 }) => (
  <div className="greeting">
    <h1>你好，{name}</h1>
    <p>年龄：{age}</p>
  </div>
);

// 使用组件
function App() {
  return (
    <div>
      <Greeting name="Alice" age={30} />
      <Greeting name="Bob" />  {/* age 使用默认值 18 */}
    </div>
  );
}

// ★ 条件渲染
function UserCard({ user }) {
  return (
    <div>
      {user ? (
        <p>{user.name}</p>
      ) : (
        <p>加载中...</p>
      )}
      
      {/* 短路 */}
      {user.isAdmin && <button>管理面板</button>}
      
      {/* 三元 */}
      <span>{user.online ? '🟢 在线' : '⚫ 离线'}</span>
    </div>
  );
}

// ★ 列表渲染
function UserList({ users }) {
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>  {/* key 必须有！且稳定唯一 */}
          {user.name} - {user.email}
        </li>
      ))}
    </ul>
  );
}

// ★ 事件处理
function SearchBox() {
  const [query, setQuery] = useState('');
  
  const handleChange = (e) => {
    setQuery(e.target.value);
  };
  
  const handleSubmit = (e) => {
    e.preventDefault(); // 阻止表单默认提交
    console.log('搜索:', query);
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={query}
        onChange={handleChange}
        placeholder="搜索..."
      />
      <button type="submit">搜索</button>
    </form>
  );
}

// 后端类比：
// 组件 ≈ Go 的函数（输入 props，输出 UI）
// 条件渲染 ≈ Go template 的 {{ if }}
// 列表渲染 ≈ Go template 的 {{ range }}
// key ≈ 数据库主键（React 用它来高效更新 DOM）
```

**5. useState（状态管理基础）**

```jsx
import { useState } from 'react';

function Counter() {
  // 状态变量 + 更新函数 + 初始值
  const [count, setCount] = useState(0);
  
  // ★ 状态更新是异步的！
  const handleIncrement = () => {
    setCount(prev => prev + 1); // 用函数形式避免闭包陷阱
  };
  
  // ★ 状态更新会触发重新渲染
  // 类似 Go 中修改了状态变量，然后重新渲染模板
  
  return (
    <div>
      <p>计数：{count}</p>
      <button onClick={handleIncrement}>+1</button>
      <button onClick={() => setCount(count - 1)}>-1</button>
      <button onClick={() => setCount(0)}>重置</button>
    </div>
  );
}

// ★ 对象/数组状态更新（不可变！）
function UserForm() {
  const [form, setForm] = useState({ name: '', email: '', role: 'user' });
  
  const updateField = (field, value) => {
    setForm(prev => ({ ...prev, [field]: value }));
    // 必须创建新对象！不能直接修改 prev
    // 类似 Go 中返回新的 struct 而不是修改原来的
  };
  
  return (
    <input
      value={form.name}
      onChange={e => updateField('name', e.target.value)}
    />
  );
}

// 后端类比：
// useState ≈ Go 中的一个变量 + 变更通知机制
// setCount ≈ 修改变量 + 通知 UI 重新渲染
// 不可变更新 ≈ Go 中值类型的赋值（int, string, struct 都是值拷贝）
```

#### 实战练习

1. **创建一个温度转换器**：摄氏度 ↔ 华氏度，双向绑定
2. **创建一个星级评分组件**：支持半星、只读模式、自定义大小
3. **创建一个标签输入组件**：输入后回车添加标签，点击 × 删除，支持退格删除

---
