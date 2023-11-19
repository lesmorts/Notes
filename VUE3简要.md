## VUE3简要

### 声明式渲染

1. reactive()
   ```js
   import { reactive } from 'vue'
   const counter = reactive({
     count: 0
   })
   
   console.log(counter.count) // 0
   counter.count++

- 适用：对象，数组，内置类型
- 返回 Proxy

2. ref()

   ```js
   import { ref } from 'vue'
   
   const message = ref('Hello World!')
   
   console.log(message.value) // "Hello World!"
   message.value = 'Changed'
   ```

- 适用：值类型

- 返回一个包裹对象，内部值在`.value`下

### Attribute绑定

  指令：

  ```html
  <div v-bind:id="dynamicId"></div>
  <div :id="dynamicId"></div>
  ```

  元素的 `id` attribute 将与组件状态里的 `dynamicId` 属性保持同步。

### 事件监听

用 `v-on` 指令监听 DOM 事件

```html
<button v-on:click="increment">{{ count }}</button>
<button @click="increment">{{ count }}</button>
```

### 表单绑定

双向绑定

```html
//同时使用 v-bind 和 v-on 来在表单的输入元素上创建双向绑定
<input :value="text" @input="onInput">
```

`v-model`语法糖

```html
<input v-model="text">
```

### 条件渲染

使用`v-if`指令有条件地渲染元素

```vue
<script setup>
import { ref } from 'vue'

const awesome = ref(true)

function toggle() {
  awesome.value = !awesome.value
}
</script>

<template>
  <button @click="toggle">toggle</button>
  <h1 v-if="awesome">Vue is awesome!</h1>
  <h1 v-else>Oh no 😢</h1>
</template>
```

### 列表渲染

使用`v-for`指令渲染基于源数组的列表

```vue
<script setup>
import { ref } from 'vue'

// 给每个 todo 对象一个唯一的 id
let id = 0

const newTodo = ref('')
const todos = ref([
  { id: id++, text: 'Learn HTML' },
  { id: id++, text: 'Learn JavaScript' },
  { id: id++, text: 'Learn Vue' }
])

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)//替换原来的元素
}
</script>

<template>
  <form @submit.prevent="addTodo">//提交时调用addTodo函数
    <input v-model="newTodo">//与newTodo绑定
    <button>Add Todo</button>    
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo.id">//通过:key绑定每个li，v-for遍历数组
      {{ todo.text }}
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
</template>
```

### 计算属性

由上一个例子，通过添加`done`属性实现隐藏完成项

```vue
<script setup>
import { ref } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Learn HTML', done: true },
  { id: id++, text: 'Learn JavaScript', done: true },
  { id: id++, text: 'Learn Vue', done: false }
])
const fileteredTodos=computed(()=>{
    returen hideCompleted?
        todos.value.filter((t)=>!t.done):todos.value
})
function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>
  </form>
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>
```

### 生命周期和模板引用

**模版引用**

```html
<p ref="pElementRef">hello</p>
```

要访问该引用，我们需要声明一个同名的 ref：

```js
const pElementRef = ref(null)
```

注意这个 ref 使用 `null` 值来初始化。这是因为当 `<script setup>` 执行时，DOM 元素还不存在。模板引用 ref 只能在组件**挂载**后访问。

要在挂载之后执行代码，我们可以使用 `onMounted()` 函数：

```js
import { onMounted } from 'vue'

onMounted(() => {
  // 此时组件已经挂载。
})
```

这被称为**生命周期钩子**

### 侦听器

```js
import { ref, watch } from 'vue'

const count = ref(0)

watch(count, (newCount) => {
  // 没错，console.log() 是一个副作用
  console.log(`new count is: ${newCount}`)
})
```

### 组件

```vue
<script setup>
import ChildComp from './ChildComp.vue'//导入
</script>

<template>
  <ChildComp />//使用
</template>
```

### Props

子组件可以通过 **props** 从父组件接受动态数据

```vue
<!-- ChildComp.vue -->
<script setup>
const props = defineProps({
  msg: String
})
</script>
```

```vue
<script setup>
import { ref } from 'vue'
import ChildComp from './ChildComp.vue'

const greeting = ref('Hello from parent')
</script>

<template>
  <ChildComp :msg="greeting" />//使用子组件定义的msg prop
</template>
```

### Emits

子组件向父组件触发事件：

`emit()` 的第一个参数是事件的名称。其他所有参数都将传递给事件监听器。

```vue
<!-- ChildComp.vue -->
<script setup>
// 声明触发的事件
const emit = defineEmits(['response'])

// 带参数触发
emit('response', 'hello from child')
</script>
```

```vue
<script setup>
import { ref } from 'vue'
import ChildComp from './ChildComp.vue'

const childMsg = ref('No child msg yet')
</script>

<template>
  <ChildComp @response="(msg)=>childMsg=msg"/>//监听触发事件，传入参数msg并赋值给本地childMsg
  <p>{{ childMsg }}</p>
</template>
```

### 插槽

父组件通过插槽(slots)将模版片段传递给子组件

子组件中`<slot>`作为插槽出口渲染父组件中的插槽内容

```vue
<!-- ChildComp.vue -->
<template>
  <slot>Fallback content</slot>
</template>
```

```vue
<script setup>
import { ref } from 'vue'
import ChildComp from './ChildComp.vue'

const msg = ref('from parent')
</script>

<template>
  <ChildComp>Message:{{msg}}</ChildComp>//通过msg添加插槽内容
</template>
```

