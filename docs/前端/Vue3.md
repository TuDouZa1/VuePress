---
title: Vue3
createTime: 2025/07/08 17:03:15
permalink: /article/xou8iee9/
---
# Vue3

> [Vue.js - 渐进式 JavaScript 框架 | Vue.js](https://cn.vuejs.org/)

## 安装和创建Vue

### 快速使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">{{ message }}</div>

    <script type="module">
        import { createApp, ref } from 'https://unpkg.com/vue@3/dist/vue.esm-browser.js'
        createApp({
                setup() {
                const message = ref('Hello Vue!')
                return {
                    message
                }
            }
        }).mount('#app')
    </script>
</body>
</html>
```

### 配置NodeJS

> [Node.js — 在任何地方运行 JavaScript](https://nodejs.org/zh-cn)

```cmd
npm config set prefix "C:\Program Files\nodejs"
npm config set registry http://registry.npm.taobao.org/
```

### 创建Vue工程

```cmd
npm init vue@latest
cd vue-project
npm install
```

### 启动Vue

- 执行 `npm run dev`
- 访问 `http://127.0.0.1:5173`

## 基础

### 响应式数据

- Vue3 使用 `ref` 和 `reactive` 来创建响应式数据。
- `ref` 用于声明一个响应式的引用，它可以包含基本数据类型。
- `reactive` 用于声明一个响应式的对象。

```javascript
import { ref, reactive } from 'vue'

export default {
  setup() {
    const count = ref(0)
    const info = reactive({
      name: 'Vue3',
      version: '3.3.4'
    })

    const increment = () => {
      count.value++
      info.version = '3.4.0'
    }

    return {
      count,
      info,
      increment
    }
  }
}
```





## Axios

> [Axios中文文档 | Axios中文网](https://www.axios-http.cn/)

### 拦截器

#### 响应拦截器

```js
import axios from 'axios';

//const baseURL = 'http://localhost:8080'
const baseURL = '/api'
const instance = axios.create({
  baseURL
})

// 添加响应拦截器
instance.interceptors.response.use(
  result => {
    if (result.data.code === 0) {
      return result.data;
    }
    alert(result.data.message ? result.data.message : '服务异常')
    return Promise.reject(result.data);
  },
  err => {
    alert('服务异常');
    return Promise.reject(err); // 异步的状态改为失败的状态
  }
);

export default instance;
```

## Element Plus

> [一个 Vue 3 UI 框架 | Element Plus](https://element-plus.org/zh-CN/#/zh-CN)

### 安装

```cmd
npm install element-plus --save
```

## 跨域

> 不同源导致的问题

```js
const baseURL = '/api'
```

vite.config.js

```js
  server: {
    proxy: {
      '/api': {
        target: 'http://localhost:8080',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, '')
      }
    }
  }
```

## 路由

> [Vue Router | Vue.js 的官方路由](https://router.vuejs.org/zh/)
> 在前端工程中，路由指的是根据不同的访问路径，展示不同组件的内容。Vue Router是Vue.js的官方路由，它与Vue.js深度集成，让Vue.js构建单页面应用变得更加轻而易举

### 安装

```cmd
npm install vue-router@4
```

## Pinia

> [Pinia | The intuitive store for Vue.js](https://pinia.vuejs.org/zh/)

### 安装

```cmd
npm install pinia
```

### Persist

> [GitHub - Seb-L/pinia-plugin-persist: Persist pinia state data in sessionStorage or other storages.](https://github.com/Seb-L/pinia-plugin-persist)

