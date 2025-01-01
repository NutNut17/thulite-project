---
title: "Vue"
description: ""
summary: ""
date: 2024-10-20T01:13:34+08:00
lastmod: 2024-10-20T01:13:34+08:00
draft: false
weight: 107
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

{{< inline-svg src="svgs/logos/vue.svg" width="100px" height="79px" class="svg-inline-custom" >}}

### Concepts

A `.vue` files may have HTML, CSS, JS template syntax inside. `<template></template>` is for HTML structure, `<style></style>` is for CSS style, `<script></script>` is for JavaScript script.

Vue have two code modes, Options and Composition Mode. But in this documentation. We use composition

| Options | Composition |
| - | - |
| Older and more structural | Newer and more flexible |
| More codes, with `export` in script for setup | Less code, using `<script setup>` |

#### Getting started

Run the code below to get started

```bash
npm install -g @vue/cli
vue create my-vue-app
cd my-vue-app
npm run dev
# or
npm run serve
# For deployment
npm run build
```

Then, select manually select feature to suits your need. Router, Pinia (global state management) is recommended. Starter template will be at [port 8080](http://localhost:8080)

```bash {title="Project Structure"}
vue-app/
├── public/
├── src/
│   ├── assets/
│   ├── components/ # For reusable components
│   │   └── ButtonComponent.vue 
│   ├── router/
│   │   └── index.js
│   ├── store/
│   │   └── index.js
│   ├── views/ # For pages
│   │   ├── HomeView.vue
│   │   └── AboutView.vue
│   ├── App.vue
│   └── main.js
├── .gitignore
├── package.json
└── vue.config.js
```

#### Tutorial

This briefly shows some fundamentals concepts on Vue in two files. The concepts are declarative rendering, attribute bindings, event listeners, form bindings, conditional rendering, list rendering, computed property, lifecycle and template refs, watchers, components, props, emits, slots.

{{< details "Show code" >}}

{{< tabs "codes" >}}

{{< tab "App.vue" >}}

```html
<!-- Only one setup can be made on each file -->
<script setup>
import { reactive, ref } from 'vue' // Import state library

// Declarative rendering: renders dynamically
const counter = reactive({ count: 0 })  // Access by counter.count
const message = ref('Hello World!')     // Access by message.value
const styleRef = ref('red')

function increment() {
  counter.count += 1
}

// Access DOM manually after elements being mounted. During script setup, the DOM is not created yet.
import { onMounted } from 'vue'

const pElementRef = ref(null)
onMounted(() => {
  pElementRef.value.textContent = 'Mounted! (DOM operation)'
})

// Making(triggers) 'side effects' reactively using watch
import { watch } from 'vue'

const todoId = ref(1)
const todoData = ref(null)

async function fetchData() {
  todoData.value = null
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
  )
  todoData.value = await res.json()
}

fetchData()

watch(todoId, fetchData)

// Import other components
import ChildComp from './ChildComp.vue'

// Define ref to receive child component data
const childMsg = ref('No child msg yet')
</script>

<template>
  <!-- Attribute Binding: ':class' is 'v-bind:class', binding class values to styleRef ref, message under mustache '{{ message }}' render dynamically to message ref -->
  <h1 :class="styleRef">{{ message }}</h1>

  <!-- Event Listeners: '@click' is 'v-on:click', calls the function 'increment() when clicked' -->
  <button @click="increment"> Count is: {{ counter.count }}</button>

  <!-- Form Binding: 'v-model:"message"'create two-way binding  -->
  <input v-model="message" placeholder="Type here">

  <!-- Conditional Rendering: 'v-if:"counter.count % 2 !== 0"'  -->
  <p v-if="counter.count % 2 !== 0">The counter is odd</p>
  <p v-else>The counter is even</p>

  <!-- Lifecycle and Template Refs: manually work with DOM -->
  <p ref="pElementRef">Hello</p>

  <!-- Watchers: trigger when reactivity data changes -->
  <p>Todo id: {{ todoId }}
    <button @click="todoId++" :disabled="!todoData">Fetch next todo</button>
  </p>
  <p v-if="!todoData">Loading...</p>
  <pre v-else>{{ todoData }}</pre>

  <!-- Import ChildComp component and prop to child component -->
  <ChildComp :propToChild="'This is a prop to child component'" @response="(msg) => childMsg = msg">
    <!-- Slots: pass down template fragments to child -->
    Message to child: {{ message }}
  </ChildComp>
  <p>{{ childMsg }}</p>

</template>

<style>
.red {
  color: red;
}
</style>
```

{{< /tab >}}
{{< tab "ChildComp.vue" >}}

```html
<script setup>
import { ref, computed } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Learn HTML', done: true },
  { id: id++, text: 'Learn JavaScript', done: true },
  { id: id++, text: 'Learn Vue', done: false }
])

// Computed property: computes its value based on other reactive data sources
const filteredTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done)
    : todos.value
})

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  // t is the item iterated in todos, filter returns list after removing item with false statement
  todos.value = todos.value.filter((t) => t !== todo)
}

// Define props to receive data from parent
const props = defineProps({
  propToChild: String
})

// Setup emit to send data to parent
const emitFromChild = defineEmits(['response'])
emitFromChild('response', 'This is an emit from child')

</script>

<template>
  <h2>{{ propToChild || 'No props passed yet' }}</h2>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo" required placeholder="new todo">
    <button>Add Todo</button>
  </form>
  <ul>
    <!-- List Rendering -->
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>

  <slot>Fallback content from parent</slot>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>
```

{{< /tab >}}
{{< /tabs >}}
{{< /details >}}

#### Router

To control and remember URL routes on the site

{{< details "Router Configurations" >}}

The structure are as below. Configure index.js, add views and make sure `main.js` imports router to be use

```js {title="src/router/index.js"}
import { createRouter, createWebHashHistory } from 'vue-router'
import HomeView from '../views/HomeView.vue'
import HomeView from '../views/LoginView.vue'

// You have two ways to configure router
const routes = [
  {
    path: '/', redirect: '/about/home', // Default route
  },
  {
    path: '/about', name: 'about',
    // Nested routes
    children: [
      { path: 'home', component: HomeView },
      { path: 'login', component: LogInView },
    ],
    // Route level code-splitting: this generates a separate chunk about.[hash].js)
    component: () => import(/* webpackChunkName: "about" */ '../views/AboutView.vue')
  },
]

const router = createRouter({
  history: createWebHashHistory(),
  routes
})

export default router
```

```vue
<script>
  import { useRouter } from 'vue-router';
  const router = useRouter();

  router.push('/path'); // Move to a route
</script>

<template>
  <router-link to="/path"><a> Link </a></router-link>
  <router-view> Router views will be rendered here </router-view>
</template>
```

```vue {title="src/views/HomeView.vue"}
<script setup>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
</script>

<template>
  <div class="home">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>
```

```vue {title="src/views/AboutView.vue"}
<template>
  <div class="about">
    <h1>This is an about page. Without importing any other components</h1>
  </div>
</template>
```

{{< /details >}}

#### Pinia

Am official global state management tool for vue

{{< details "Pinia Configurations" >}}

Install pinia through npm

```js {title="src/store/index.js"}
import { defineStore } from 'pinia';

export const useGlobalStore = defineStore('global', {
  state: () => ({
    // The global value
    value: null, 
    uname: null
  }),
  getters: {
    getValue: (state) => state.value,
    getUname: (state) => state.uname
  },
  actions: {
    setValue(newValue) {
      this.value = newValue;
    },
    setUname(uname) {
      this.uname = uname;
    },
    clear() {
      this.value = null;
      this.uname = null;
    }
  },
});
```

{{< /details >}}

### PrimeVue

Primevue is a framework to make modern UI by adding components into vue files. Visit [PrimeVue](https://primevue.org/introduction/) to get started.
