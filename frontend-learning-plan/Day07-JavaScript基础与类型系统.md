# Day 7：JavaScript 基础与类型系统

#### 学习内容

**1. 变量声明（★★★ 重点理解区别）**

```javascript
// var — 函数作用域，变量提升（避免使用！）
function example() {
  console.log(x); // undefined（不会报错，因为变量提升）
  var x = 10;
}

// let — 块级作用域，暂时性死区（推荐）
function example() {
  // console.log(x); // ReferenceError!
  let x = 10;
  if (true) {
    let y = 20; // 只在 if 块内可见
  }
  // console.log(y); // ReferenceError!
}

// const — 块级作用域，必须初始化，不能重新赋值（推荐）
const PI = 3.14;
// PI = 3; // TypeError!

// ⚠️ const 不是不可变！对象/数组的属性可以修改
const arr = [1, 2, 3];
arr.push(4);      // ✅ 可以
arr = [5, 6];     // ❌ TypeError!

const obj = { name: 'Alice' };
obj.name = 'Bob'; // ✅ 可以
obj = {};         // ❌ TypeError!

// 后端类比：
// let ≈ Go 的 :=（短变量声明）
// const ≈ Go 的 const（但更灵活）
// var ≈ 没有对应（Go 没有变量提升这种概念）
```

**2. 数据类型**

```javascript
// === 原始类型（Primitive）===
typeof 42;           // "number"
typeof "hello";      // "string"
typeof true;         // "boolean"
typeof undefined;    // "undefined"
typeof null;         // "object" ← 历史遗留 bug！用 === null 判断
typeof Symbol();     // "symbol"
typeof 42n;          // "bigint"
typeof function(){}; // "function" ← 不是原始类型，但 typeof 返回这个

// === 引用类型 ===
typeof {};           // "object"
typeof [];           // "object" ← 数组也是对象！用 Array.isArray() 判断
typeof null;         // "object" ← 又是这个 bug

// === 类型转换陷阱（★★★ 面试高频）===
// 隐式转换规则：
"5" + 3;     // "53"（字符串拼接）
"5" - 3;     // 2（数学运算）
"5" * 3;     // 15
"5" == 5;    // true（宽松相等，会类型转换）
"5" === 5;   // false（严格相等，推荐！）
null == undefined;  // true
null === undefined; // false
[] == false;  // true（各种隐式转换...）
[] == ![];    // true（经典面试题）

// ★ 永远用 === 严格相等！
```

**3. 解构赋值（ES6+）**

```javascript
// 数组解构
const [a, b, c] = [1, 2, 3];
const [first, ...rest] = [1, 2, 3, 4]; // first=1, rest=[2,3,4]
const [, second] = [1, 2, 3];          // 跳过第一个

// 对象解构
const { name, age } = { name: 'Alice', age: 30 };
const { name: userName, age: userAge } = obj; // 重命名
const { name = 'default' } = {};       // 默认值

// 嵌套解构
const { address: { city, zip } } = user;

// 函数参数解构（★★★ 超常用）
function createUser({ name, age, role = 'user' }) {
  return { name, age, role };
}
createUser({ name: 'Alice', age: 30 });

// 后端类比：类似 Go 的多重赋值，但更灵活
// Go: a, b := 1, 2
// JS: const [a, b] = [1, 2]
```

**4. 展开运算符（Spread / Rest）**

```javascript
// 数组展开
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5]; // [1,2,3,4,5]
const merged = [...arr1, ...arr2];

// 对象展开（浅拷贝）
const defaults = { theme: 'light', lang: 'zh', debug: false };
const userConfig = { theme: 'dark', lang: 'en' };
const config = { ...defaults, ...userConfig };
// { theme: 'dark', lang: 'en', debug: false }

// Rest 参数
function sum(...numbers) {
  return numbers.reduce((acc, n) => acc + n, 0);
}
sum(1, 2, 3, 4); // 10

// 后端类比：展开运算符 ≈ Go 的 ... 操作符
```

**5. 模板字符串**

```javascript
const name = 'Alice';
const age = 30;

// 基础
const greeting = `你好，${name}！你今年 ${age} 岁。`;

// 表达式
const info = `${name} 是${age >= 18 ? '成年' : '未成年'}人`;

// 多行
const html = `
  <div class="card">
    <h2>${name}</h2>
    <p>年龄：${age}</p>
  </div>
`;

// 标签模板（高级用法）
function highlight(strings, ...values) {
  return strings.reduce((result, str, i) => {
    return result + str + (values[i] ? `<mark>${values[i]}</mark>` : '');
  }, '');
}
highlight`搜索 ${keyword} 的结果`; // keyword 会被 <mark> 包裹
```

#### 实战练习

1. **类型判断函数**：写一个 `deepTypeOf(value)` 函数，能正确区分 `null`、`[]`、`{}`、`Date`、`RegExp` 等
2. **解构练习**：从 API 返回的嵌套 JSON 中提取特定字段
3. **对象合并工具**：实现一个 `deepMerge(target, ...sources)` 深合并函数

---
