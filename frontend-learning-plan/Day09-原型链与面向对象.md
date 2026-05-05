# Day 9：原型链与面向对象

#### 学习内容

**1. 原型链（Prototype Chain — JS 的继承机制）**

```javascript
// 每个对象都有一个内部属性 [[Prototype]]
// 通过 __proto__ 或 Object.getPrototypeOf() 访问
// 通过 Object.create() 设置

// 原型链查找过程：
const arr = [1, 2, 3];
arr.hasOwnProperty('length'); // false
// 查找顺序：arr 自身 → Array.prototype → Object.prototype → null

// Array.prototype 上有：push, pop, map, filter, reduce...
// Object.prototype 上有：toString, hasOwnProperty, valueOf...

// ★ 经典图解：
// arr → Array.prototype → Object.prototype → null
//   (push, map...)    (toString...)      (终点)

// 后端类比：
// 原型链 ≈ Go 的结构体嵌入（embedding）
// type Animal struct { Name string }
// type Dog struct { Animal }  // Dog 继承 Animal 的方法
// 但 JS 的原型链是运行时的，Go 的嵌入是编译时的
```

**2. ES6 Class（语法糖）**

```javascript
// ES6 class 本质上是构造函数 + 原型链的语法糖
class Animal {
  // 构造函数
  constructor(name) {
    this.name = name;
  }
  
  // 实例方法（挂在原型上）
  speak() {
    console.log(`${this.name} makes a sound.`);
  }
  
  // 静态方法（挂在类上，类似 Go 的包级函数）
  static create(name) {
    return new Animal(name);
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name); // 调用父类构造函数（必须！）
    this.breed = breed;
  }
  
  // 重写父类方法
  speak() {
    console.log(`${this.name} barks!`);
  }
  
  // 新方法
  fetch(item) {
    console.log(`${this.name} fetches the ${item}.`);
  }
}

const dog = new Dog('Rex', 'German Shepherd');
dog.speak();   // "Rex barks!"
dog.fetch('ball'); // "Rex fetches the ball."
dog instanceof Dog;    // true
dog instanceof Animal; // true

// Getter / Setter
class User {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
  
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
  
  set fullName(name) {
    const [first, last] = name.split(' ');
    this.firstName = first;
    this.lastName = last;
  }
}

// 私有字段（2022+）
class BankAccount {
  #balance = 0; // # 开头表示私有字段
  
  deposit(amount) {
    if (amount > 0) this.#balance += amount;
  }
  
  get balance() {
    return this.#balance;
  }
}

// 后端类比：
// class ≈ Go 的 struct + 方法集
// extends ≈ Go 的嵌入
// private fields ≈ Go 的小写字母私有字段
// getter/setter ≈ Go 没有对应（Go 不推荐 getter/setter）
```

**3. 常用内置对象方法**

```javascript
// === Object 静态方法 ===
Object.keys(obj);           // 获取所有键
Object.values(obj);         // 获取所有值
Object.entries(obj);        // 获取键值对数组
Object.assign(target, src); // 浅合并
Object.freeze(obj);         // 冻结（不可修改）
Object.seal(obj);           // 密封（不可添加/删除属性）

// === 数组高阶方法（★★★ 每天都在用）===
const users = [
  { name: 'Alice', age: 30, role: 'admin' },
  { name: 'Bob', age: 25, role: 'user' },
  { name: 'Charlie', age: 35, role: 'admin' },
];

// map — 映射转换（类似 Go 没有直接对应，需要 for range）
const names = users.map(u => u.name); // ['Alice', 'Bob', 'Charlie']

// filter — 过滤
const admins = users.filter(u => u.role === 'admin');

// find — 查找第一个匹配
const bob = users.find(u => u.name === 'Bob');

// some — 是否存在匹配
const hasAdmin = users.some(u => u.role === 'admin'); // true

// every — 是否全部匹配
const allAdults = users.every(u => u.age >= 18); // true

// reduce — 累积计算（★★★ 超强大）
const totalAge = users.reduce((sum, u) => sum + u.age, 0); // 90
const grouped = users.reduce((acc, u) => {
  (acc[u.role] = acc[u.role] || []).push(u);
  return acc;
}, {}); // { admin: [...], user: [...] }

// flatMap — 映射 + 扁平化
const nested = [[1, 2], [3, 4], [5]];
nested.flat();           // [1,2,3,4,5]
users.flatMap(u => u.hobbies || []); // 扁平化获取所有爱好

// sort — 排序（注意：原地修改！）
users.sort((a, b) => a.age - b.age); // 按年龄升序
[3, 1, 2].sort((a, b) => a - b);    // [1, 2, 3]

// 后端类比：
// map ≈ 遍历 slice 生成新 slice
// filter ≈ 遍历 slice 过滤
// reduce ≈ 遍历 slice 累积（Go 没有内置，需要手写）
// find ≈ 遍历 slice 查找
```

#### 实战练习

1. **实现一个简易的 ORM**：用 class + 原型链实现 `Model.find()`、`Model.where()`、`Model.first()` 链式调用
2. **数组方法练习**：用 `reduce` 实现 `map`、`filter`、`groupBy`、`uniq`、`flatten`
3. **深拷贝函数**：实现 `deepClone(obj)`，处理循环引用

---
