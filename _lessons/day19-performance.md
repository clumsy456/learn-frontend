---
layout: default
title: "Day 19：性能优化"
categories: ['进阶', '第四周']
tags: ['性能优化', '懒加载', '缓存']
---

#### 学习内容

**1. 渲染性能**

```jsx
// ★ React.memo — 避免不必要的重新渲染
const ExpensiveList = React.memo(function ExpensiveList({ items }) {
  return items.map(item => <ListItem key={item.id} item={item} />);
});

// ★ useMemo — 缓存计算结果
function UserDashboard({ users, filter }) {
  const filteredUsers = useMemo(() => {
    return users.filter(u => u.name.includes(filter));
  }, [users, filter]); // 只有 users 或 filter 变化时重新计算
  
  return <UserList users={filteredUsers} />;
}

// ★ useCallback — 缓存函数引用
function Parent() {
  const [count, setCount] = useState(0);
  
  const handleClick = useCallback(() => {
    console.log('clicked');
  }, []); // 空依赖 = 函数永远不会变
  
  return <Child onClick={handleClick} />;
}

// 后端类比：
// React.memo ≈ Go 的 sync.Pool（复用对象，减少分配）
// useMemo ≈ Go 的缓存（避免重复计算）
// useCallback ≈ Go 中缓存函数引用
```

**2. 代码分割与懒加载**

```jsx
import { lazy, Suspense } from 'react';

// 路由级懒加载（最常用）
const Home = lazy(() => import('./pages/Home'));
const Admin = lazy(() => import('./pages/Admin'));

function App() {
  return (
    <Suspense fallback={<Loading />}>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/admin" element={<Admin />} />
      </Routes>
    </Suspense>
  );
}

// 组件级懒加载
const HeavyChart = lazy(() => import('./components/HeavyChart'));

function Dashboard() {
  const [showChart, setShowChart] = useState(false);
  
  return (
    <div>
      <button onClick={() => setShowChart(true)}>显示图表</button>
      {showChart && (
        <Suspense fallback={<div>加载图表中...</div>}>
          <HeavyChart />
        </Suspense>
      )}
    </div>
  );
}

// 后端类比：
// 代码分割 ≈ Go 的 plugin 模式（按需加载）
// 懒加载 ≈ Go 的延迟初始化（sync.Once）
```

**3. 关键性能指标（Core Web Vitals）**

```
LCP (Largest Contentful Paint) — 最大内容绘制 < 2.5s
FID (First Input Delay) — 首次输入延迟 < 100ms
CLS (Cumulative Layout Shift) — 累积布局偏移 < 0.1
INP (Interaction to Next Paint) — 交互到下次绘制 < 200ms

优化手段：
- 图片优化：WebP 格式、懒加载、响应式图片、CDN
- 代码分割：路由懒加载、动态 import
- 缓存策略：Service Worker、HTTP 缓存头
- 渲染优化：虚拟列表、防抖节流、避免强制同步布局
- 资源优化：Tree Shaking、压缩、预加载
```

**4. 虚拟列表（Virtual List）**

```jsx
// 当列表有上千条数据时，只渲染可视区域的元素
import { useVirtualizer } from '@tanstack/react-virtual';

function VirtualList({ items }) {
  const parentRef = useRef(null);
  
  const virtualizer = useVirtualizer({
    count: items.length,
    getScrollElement: () => parentRef.current,
    estimateSize: () => 50, // 每项高度
    overscan: 5, // 额外渲染 5 项
  });
  
  return (
    <div ref={parentRef} style={{ height: '600px', overflow: 'auto' }}>
      <div style={{ height: `${virtualizer.getTotalSize()}px` }}>
        {virtualizer.getVirtualItems().map(virtualItem => (
          <div
            key={virtualItem.key}
            style={{
              position: 'absolute',
              top: 0,
              transform: `translateY(${virtualItem.start}px)`,
              height: `${virtualItem.size}px`,
            }}
          >
            {items[virtualItem.index].name}
          </div>
        ))}
      </div>
    </div>
  );
}
```

#### 实战练习

1. **用 React DevTools Profiler 分析组件渲染性能**：找出不必要的重新渲染
2. **实现一个虚拟滚动列表**：渲染 10000 条数据，保持 60fps
3. **用 Lighthouse 审计你的博客项目**：优化到 90+ 分
