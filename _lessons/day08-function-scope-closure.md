---
layout: default
title: "Day 8：函数、作用域与闭包"
categories: ['JavaScript', '第二周']
tags: ['javascript', '闭包', '作用域']
---

#### 学习内容

**1. 函数定义方式**

```javascript
// 函数声明（有提升）
function add(a, b) { return a + b; }

// 函数表达式（无提升）
const add = function(a, b) { return a + b; };

// 箭头函数（★★★ 最常用）
const add = (a, b) => a + b;
const square = x => x * x;
const getObj = () => ({ key: 'value' }); // 返回对象要加括号

// 箭头函数 vs 普通函数的区别：
// 1. 没有 this 绑定（继承外层 this）
// 2. 没有 arguments 对象
// 3. 不能用作构造函数（不能 new）
// 4. 没有 prototype 属性

// ★ 后端类比：箭头函数 ≈ Go 的匿名函数
// Go: func(x int) int { return x * x }
// JS: x => x * x
```

**2. 默认参数与剩余参数**

```javascript
// 默认参数
function fetch(url, method = 'GET', headers = {}) {
  // ...
}
fetch('/api/users');           // method='GET', headers={}
fetch('/api/users', 'POST');   // headers={}

// 剩余参数
function log(level, ...messages) {
  console.log(`[${level}]`, ...messages);
}
log('INFO', '请求开始', 'URL:', url);

// 后端类比：类似 Go 的可变参数
// Go: func log(level string, msgs ...string)
```

**3. 作用域链**

```javascript
// 全局作用域
let globalVar = 'global';

function outer() {
  // 函数作用域
  let outerVar = 'outer';
  
  function inner() {
    // 内层函数作用域
    let innerVar = 'inner';
    
    console.log(innerVar);  // ✅ 'inner'
    console.log(outerVar);  // ✅ 'outer'（沿作用域链向上查找）
    console.log(globalVar); // ✅ 'global'
  }
  
  inner();
  // console.log(innerVar); // ❌ ReferenceError
}

outer();
// 后端类比：类似 Go 的作用域规则，但 JS 有函数作用域（Go 只有块作用域）
```

**4. 闭包（Closure — ★★★ 核心概念）**

```javascript
// 闭包 = 函数 + 它能访问的外层变量
function createCounter() {
  let count = 0; // 被闭包"捕获"的变量
  
  return {
    increment: () => ++count,
    decrement: () => --count,
    getCount: () => count,
  };
}

const counter = createCounter();
counter.increment(); // 1
counter.increment(); // 2
counter.getCount();  // 2
// count 变量在外部无法直接访问，只能通过返回的方法操作
// ★ 这就是"数据私有化"——类似 Go 的私有字段

// 实际应用：防抖（Debounce）
function debounce(fn, delay) {
  let timer = null;
  return function(...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}
const search = debounce(query => fetchResults(query), 300);
input.addEventListener('input', e => search(e.target.value));

// 实际应用：节流（Throttle）
function throttle(fn, interval) {
  let lastTime = 0;
  return function(...args) {
    const now = Date.now();
    if (now - lastTime >= interval) {
      lastTime = now;
      fn.apply(this, args);
    }
  };
}
const onScroll = throttle(() => updatePosition(), 100);
window.addEventListener('scroll', onScroll);

// 实际应用：缓存（Memoize）
function memoize(fn) {
  const cache = new Map();
  return function(...args) {
    const key = JSON.stringify(args);
    if (cache.has(key)) return cache.get(key);
    const result = fn.apply(this, args);
    cache.set(key, result);
    return result;
  };
}
const expensiveCalc = memoize(n => {
  console.log('计算中...');
  return n * n;
});
expensiveCalc(5); // "计算中..." → 25
expensiveCalc(5); // 25（直接从缓存取）

// 后端类比：
// 闭包 ≈ Go 的闭包（概念相同）
// 防抖 ≈ Go 中带 timer 的 rate limiter
// 节流 ≈ Go 中 time.Ticker
// 缓存 ≈ sync.Map 或带锁的 map
```

**5. this 关键字（★★★ JS 最令人困惑的概念）**

```javascript
// this 的值取决于函数如何被调用（不是定义位置！）

// 1. 全局上下文
console.log(this); // window（浏览器）/ global（Node）

// 2. 对象方法
const user = {
  name: 'Alice',
  greet() {
    console.log(this.name); // 'Alice' — this 指向调用对象
  }
};
user.greet(); // 'Alice'

// 3. 箭头函数（继承外层 this）
const user = {
  name: 'Alice',
  greet: () => {
    console.log(this.name); // undefined — this 不指向 user！
  },
  greetLater() {
    setTimeout(() => {
      console.log(this.name); // 'Alice' — 箭头函数继承 greetLater 的 this
    }, 100);
  }
};

// 4. 回调函数中的 this 丢失
class Button {
  constructor(label) {
    this.label = label;
  }
  // ❌ 错误：this 丢失
  // onClick() { console.log(this.label); }
  
  // ✅ 方案1：箭头函数
  onClick = () => console.log(this.label);
  
  // ✅ 方案2：bind
  // constructor() { this.onClick = this.onClick.bind(this); }
}

// 5. 显式绑定
function greet(greeting) {
  console.log(`${greeting}, ${this.name}`);
}
greet.call({ name: 'Alice' }, 'Hello');  // "Hello, Alice"
greet.apply({ name: 'Bob' }, ['Hi']);     // "Hi, Bob"
const boundGreet = greet.bind({ name: 'Charlie' });
boundGreet('Hey'); // "Hey, Charlie"

// 后端类比：
// JS 的 this ≈ Go 的 receiver（方法接收者）
// 但 JS 的 this 更灵活（也更混乱），Go 的 receiver 是编译时确定的
```

#### 实战练习

1. **实现一个 EventEmitter**：支持 `on`、`off`、`emit`、`once` 方法
2. **实现 curry 函数**：`curry(add)(1)(2)` → `3`
3. **实现 compose 函数**：`compose(fn1, fn2, fn3)(x)` → `fn1(fn2(fn3(x)))`
