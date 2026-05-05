# Day 16：Vue 3 核心概念（快速了解）

> **建议**：主攻 React，但了解 Vue 3 的核心概念，拓宽视野

```vue
<!-- Vue 3 组合式 API（Composition API） -->
<script setup>
import { ref, reactive, computed, watch, onMounted } from 'vue'

// ref — 基本类型响应式（类似 React 的 useState）
const count = ref(0)
const name = ref('Alice')

// reactive — 对象响应式
const user = reactive({
  name: 'Alice',
  age: 30,
  hobbies: ['coding', 'reading'],
})

// computed — 计算属性（有缓存）
const doubleCount = computed(() => count.value * 2)
const fullName = computed(() => `${user.name}, ${user.age}岁`)

// watch — 侦听器
watch(count, (newVal, oldVal) => {
  console.log(`count: ${oldVal} → ${newVal}`)
})

watch(() => user.name, (newName) => {
  console.log('名字变了:', newName)
})

// 生命周期
onMounted(() => {
  console.log('组件挂载了')
})

// 方法
function increment() {
  count.value++ // 注意要 .value！
}
</script>

<template>
  <!-- 模板语法 -->
  <div>
    <p>{{ name }}</p>
    <p>计数：{{ count }}（双倍：{{ doubleCount }}）</p>
    <button @click="increment">+1</button>
    
    <!-- v-if 条件渲染 -->
    <p v-if="count > 10">大于10</p>
    <p v-else-if="count > 5">大于5</p>
    <p v-else>小于等于5</p>
    
    <!-- v-for 列表渲染 -->
    <ul>
      <li v-for="hobby in user.hobbies" :key="hobby">
        {{ hobby }}
      </li>
    </ul>
    
    <!-- v-model 双向绑定（React 没有这个！） -->
    <input v-model="name" placeholder="输入名字">
    
    <!-- v-show（display:none，不销毁 DOM） -->
    <div v-show="count > 0">可见</div>
  </div>
</template>

<style scoped>
/* scoped 样式只作用于当前组件 */
p { color: #333; }
</style>
```

**React vs Vue 对比（后端工程师视角）**

| 特性 | React | Vue |
|------|-------|-----|
| 模板 | JSX（JS 中写 HTML） | Template（HTML 中写 JS） |
| 状态 | useState | ref / reactive |
| 副作用 | useEffect | watch / onMounted |
| 计算属性 | useMemo | computed |
| 双向绑定 | 手动（value + onChange） | v-model（内置） |
| 生态 | 更大、更灵活 | 更统一、更易上手 |
| TypeScript | 原生支持 | 良好支持 |
| 学习曲线 | 较陡（JSX + Hooks 概念多） | 较缓（模板更直观） |

---
