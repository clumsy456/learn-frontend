---
layout: default
title: "Day 14：React 进阶（useEffect、useRef、自定义 Hook）"
categories: ['框架', '工程化', '第三周']
tags: ['react', 'hooks', 'useEffect']
---

#### 学习内容

**1. useEffect（副作用处理）**

```jsx
import { useState, useEffect } from 'react';

// ★ 基础用法（每次渲染后执行）
function Timer() {
  const [count, setCount] = useState(0);
  
  useEffect(() => {
    console.log('组件渲染了');
  }); // 没有依赖数组 = 每次渲染都执行（通常不是你想要的）
  
  return <p>{count}</p>;
}

// ★ 空依赖数组（只在挂载时执行一次）
function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  
  useEffect(() => {
    // 组件挂载时执行（类似 Go 的 init 或 Python 的 __init__）
    fetch(`/api/users/${userId}`)
      .then(res => res.json())
      .then(setUser);
  }, []); // 空数组 = 只执行一次
  
  if (!user) return <p>加载中...</p>;
  return <p>{user.name}</p>;
}

// ★ 有依赖（依赖变化时执行）
function SearchResults({ query }) {
  const [results, setResults] = useState([]);
  
  useEffect(() => {
    if (!query) return;
    
    // 防抖搜索
    const timer = setTimeout(() => {
      fetch(`/api/search?q=${query}`)
        .then(res => res.json())
        .then(setResults);
    }, 300);
    
    // ★★★ 清理函数（重要！）
    return () => clearTimeout(timer);
    // 下次 effect 执行前 / 组件卸载时调用
    // 类似 Go 的 defer
  }, [query]); // query 变化时重新执行
  
  return (
    <ul>
      {results.map(r => <li key={r.id}>{r.title}</li>)}
    </ul>
  );
}

// ★ 常见 useEffect 模式

// 1. 订阅/取消订阅
useEffect(() => {
  const ws = new WebSocket('wss://api.example.com');
  ws.onmessage = (e) => handleMessage(JSON.parse(e.data));
  return () => ws.close(); // 清理
}, []);

// 2. 事件监听
useEffect(() => {
  const handler = (e) => { /* ... */ };
  window.addEventListener('resize', handler);
  return () => window.removeEventListener('resize', handler);
}, []);

// 3. 定时器
useEffect(() => {
  const id = setInterval(() => setCount(c => c + 1), 1000);
  return () => clearInterval(id);
}, []);

// 后端类比：
// useEffect(fn, []) ≈ Go 的 init() 函数
// useEffect(fn, [dep]) ≈ Go 中监听 channel，当数据变化时触发
// cleanup ≈ Go 的 defer
```

**2. useRef**

```jsx
import { useRef } from 'react';

// 1. 引用 DOM 元素
function AutoFocusInput() {
  const inputRef = useRef(null);
  
  useEffect(() => {
    inputRef.current.focus(); // 直接操作 DOM
  }, []);
  
  return <input ref={inputRef} placeholder="自动聚焦" />;
}

// 2. 存储不触发渲染的值
function StopWatch() {
  const timerRef = useRef(null);
  const [seconds, setSeconds] = useState(0);
  
  const start = () => {
    timerRef.current = setInterval(() => {
      setSeconds(s => s + 1);
    }, 1000);
  };
  
  const stop = () => clearInterval(timerRef.current);
  
  // ★ useRef vs useState：
  // useRef 修改不触发重新渲染
  // useState 修改触发重新渲染
  // 后端类比：useRef ≈ Go 的全局变量（不通知 UI），useState ≈ 响应式变量
}

// 3. 存储上一个值
function usePrevious(value) {
  const ref = useRef(value);
  useEffect(() => {
    ref.current = value;
  }, [value]);
  return ref.current;
}
```

**3. 自定义 Hook（★★★ React 的核心模式）**

```jsx
// ★ 封装可复用的逻辑
function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(() => {
    const stored = localStorage.getItem(key);
    return stored ? JSON.parse(stored) : initialValue;
  });
  
  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);
  
  return [value, setValue];
}

// 使用
function Settings() {
  const [theme, setTheme] = useLocalStorage('theme', 'light');
  const [lang, setLang] = useLocalStorage('lang', 'zh');
  
  return (
    <select value={theme} onChange={e => setTheme(e.target.value)}>
      <option value="light">亮色</option>
      <option value="dark">暗色</option>
    </select>
  );
}

// ★ 更多实用自定义 Hook

// useFetch — 数据请求
function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  
  useEffect(() => {
    setLoading(true);
    fetch(url)
      .then(res => res.json())
      .then(setData)
      .catch(setError)
      .finally(() => setLoading(false));
  }, [url]);
  
  return { data, loading, error };
}

// useDebounce — 防抖值
function useDebounce(value, delay) {
  const [debounced, setDebounced] = useState(value);
  useEffect(() => {
    const timer = setTimeout(() => setDebounced(value), delay);
    return () => clearTimeout(timer);
  }, [value, delay]);
  return debounced;
}

// useClickOutside — 点击外部
function useClickOutside(ref, handler) {
  useEffect(() => {
    const listener = (e) => {
      if (!ref.current || ref.current.contains(e.target)) return;
      handler(e);
    };
    document.addEventListener('mousedown', listener);
    return () => document.removeEventListener('mousedown', listener);
  }, [ref, handler]);
}

// 后端类比：
// 自定义 Hook ≈ Go 的中间件 / 装饰器模式
// 封装通用逻辑，在多个组件间复用
```

#### 实战练习

1. **实现 `useFetch` Hook**：支持取消请求（AbortController）、缓存、重试
2. **实现 `useInfiniteScroll` Hook**：用 IntersectionObserver 实现无限滚动
3. **实现 `useMediaQuery` Hook**：响应式媒体查询
