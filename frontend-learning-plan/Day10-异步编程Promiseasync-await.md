# Day 10：异步编程（Promise / async-await）

#### 学习内容

> **这是前端最重要的概念之一！** 后端工程师必须彻底理解事件循环。

**1. 回调地狱 → Promise → async/await**

```javascript
// ❌ 回调地狱（Callback Hell）
getUser(id, (user) => {
  getOrders(user.id, (orders) => {
    getOrderDetail(orders[0].id, (detail) => {
      getProduct(detail.productId, (product) => {
        console.log(product);
      });
    });
  });
});

// ✅ Promise 链
getUser(id)
  .then(user => getOrders(user.id))
  .then(orders => getOrderDetail(orders[0].id))
  .then(detail => getProduct(detail.productId))
  .then(product => console.log(product))
  .catch(err => console.error(err));

// ✅✅ async/await（最推荐 — 看起来像同步代码）
async function showProduct(id) {
  try {
    const user = await getUser(id);
    const orders = await getOrders(user.id);
    const detail = await getOrderDetail(orders[0].id);
    const product = await getProduct(detail.productId);
    console.log(product);
  } catch (err) {
    console.error(err);
  }
}

// 后端类比：
// 回调 ≈ Go 的 callback 模式（早期 RPC）
// Promise ≈ Go 的 channel（都可以 .then 等待结果）
// async/await ≈ Go 的 goroutine + channel（看起来都是顺序代码）
// 但！Go 是真并行（多线程），JS 是伪并行（单线程事件循环）
```

**2. Promise 详解**

```javascript
// 创建 Promise
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

function fetchUser(id) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (id > 0) {
        resolve({ id, name: 'Alice' });
      } else {
        reject(new Error('Invalid ID'));
      }
    }, 1000);
  });
}

// Promise 状态：pending → fulfilled / rejected（不可逆）

// 静态方法
Promise.all([p1, p2, p3]);       // 全部成功才成功（并行）
Promise.allSettled([p1, p2, p3]); // 全部完成（不管成功失败）
Promise.race([p1, p2]);          // 第一个完成的结果
Promise.any([p1, p2]);           // 第一个成功的结果

// 并行请求（★★★ 实际开发最常用）
async function loadDashboard() {
  const [user, orders, notifications] = await Promise.all([
    fetchUser(1),
    fetchOrders(1),
    fetchNotifications(1),
  ]);
  // 三个请求并行执行，总时间 = 最慢的那个
}

// 后端类比：
// Promise.all ≈ Go 的 errgroup.Group（WaitGroup）
// Promise.race ≈ Go 的 select + channel
// Promise.allSettled ≈ 没有直接对应（Go 需要自己实现）
```

**3. 事件循环（Event Loop — ★★★ 必须理解）**

```javascript
console.log('1'); // 同步

setTimeout(() => {
  console.log('2'); // 宏任务（Macrotask）
}, 0);

Promise.resolve().then(() => {
  console.log('3'); // 微任务（Microtask）
});

console.log('4'); // 同步

// 输出顺序：1, 4, 3, 2
// 原因：
// 1. 执行同步代码 → 输出 1, 4
// 2. 清空微任务队列 → 输出 3
// 3. 取一个宏任务执行 → 输出 2

// ★ 事件循环执行顺序：
// 同步代码 → 微任务 → 渲染 → 宏任务 → 微任务 → 渲染 → ...

// 宏任务（Macrotask）：setTimeout, setInterval, I/O, UI rendering
// 微任务（Microtask）：Promise.then, MutationObserver, queueMicrotask

// 后端类比：
// 事件循环 ≈ Go 的 runtime scheduler
// 但 Go 有 M:N 调度（多线程），JS 是单线程
// 微任务 ≈ Go 中更高优先级的 goroutine

// ★ 经典面试题
async function async1() {
  console.log('async1 start');
  await async2();
  console.log('async1 end');
}
async function async2() {
  console.log('async2');
}
console.log('script start');
setTimeout(() => console.log('setTimeout'), 0);
async1();
console.log('script end');

// 输出：script start, async1 start, async2, script end, async1 end, setTimeout
```

**4. 实用异步模式**

```javascript
// 带超时的请求
function fetchWithTimeout(url, timeout = 5000) {
  return Promise.race([
    fetch(url),
    new Promise((_, reject) =>
      setTimeout(() => reject(new Error('Timeout')), timeout)
    ),
  ]);
}

// 重试机制
async function fetchWithRetry(url, retries = 3, delay = 1000) {
  for (let i = 0; i < retries; i++) {
    try {
      return await fetch(url);
    } catch (err) {
      if (i === retries - 1) throw err;
      await new Promise(r => setTimeout(r, delay * (i + 1))); // 指数退避
    }
  }
}

// 并发控制（限制同时执行的 Promise 数量）
async function asyncPool(limit, items, fn) {
  const results = [];
  const executing = new Set();
  
  for (const item of items) {
    const p = fn(item).then(r => {
      executing.delete(p);
      return r;
    });
    executing.add(p);
    results.push(p);
    
    if (executing.size >= limit) {
      await Promise.race(executing);
    }
  }
  
  return Promise.all(results);
}

// 后端类比：
// 带超时 ≈ Go 的 context.WithTimeout
// 重试 ≈ Go 的 retry 模式
// 并发控制 ≈ Go 的 buffered channel + worker pool
```

#### 实战练习

1. **事件循环预测题**：写出 10 道复杂的事件循环输出题并验证答案
2. **实现一个 async queue**：支持 `enqueue(asyncFn)` 和 `drain()`，按顺序执行
3. **实现 `Promise.all`、`Promise.race`、`Promise.allSettled`**（不用原生 API）

---
