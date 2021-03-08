# Provider

通过 Provider，可以将 Service 提供给有需求的逻辑代码模块（组件、另一个 Service 等）。在 bizic.js 中，我们将 Provider 分为了两类：
- Root Provider，即根 Provider。
- Scoped Provider，即局部 Provider。

Provider 实际使用中，会依附组件树，形成一个由 Root Provider 为根节点的 Provider Tree.

## Root Provider

Root Provider 为根 Provider，每一个 App 实例只有一个 Root Provider。

通过 `withRootProvider(component, bizic)` 来创建一个 RootProvider 组件，如：

<!-- tabs:start -->

### **Vue 3.x**

```js
import { createApp } from 'vue';
import Bizic from 'bizic';
import { withRootProvider } from 'bizic-vue';
import App from './App.vue';

const bizic = new Bizic();
// App.vue 组件下所有的子组件都可以获取到 RootProvider 提供的 Service
const AppWithProvider = withRootProvider(App, bizic); 
const app = createApp(AppWithProvider);

app.mount('#app');

```
### **Vue 2.x**

?> TODO

<!-- tabs:end -->

## Scoped Provider

Scoped Provider，即局部 Provider，每个 App 实例可以有多个 Scoped Provider，每一个 Scoped Provider 的祖先 Provider 必须是 Root Provider。

通过 `withScopedProvider(component, scopedId)` 可以创建一个 ScopedProvider 组件，如在配置路由表时:

<!-- tabs:start -->

### **Vue 3.x**

```js
import { createRouter, createWebHistory } from 'vue-router';
import { withScopedProvider } from 'bizic-vue';
import Home from '../views/Home.vue';

const routes = [
  {
    path: '/',
    name: 'Home',
    //Home.vue 组件下都可以获取到 ScopedProvider id 为 home 的 service
    component: withScopedProvider(Home, 'home'), 
  }
];

const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes,
});

export default router;
```

### **Vue 2.x**

?> TODO

<!-- tabs:end -->
