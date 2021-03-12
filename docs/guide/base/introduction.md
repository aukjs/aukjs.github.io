# 介绍

## Bizic.js 是什么

bizic.js（business logic 的缩写）是一个基于DI的轻量级前端框架，专注于业务逻辑。解构视图逻辑和业务了逻辑，为你的项目逻辑组织提供更有力的支撑。

## 示例

<!-- tabs:start -->
### **Vue 3.x**

####  main.js

```js
import { createApp } from 'vue';
import Bizic from 'bizic';
import { withRootProvider } from 'bizic-vue';
import App from './App.vue';

const bizic = new Bizic();

// 注册 service
bizic.registerServiceFactory('foo', () => ({ bar: 'Welcome to Your Bizic.js App' }));

const AppWithProvider = withRootProvider(App, bizic);
const app = createApp(AppWithProvider);

app.mount('#app');
```

我们通过 `bizic.registerServiceFactory('foo', () => ({ bar: 'Welcome to Your Bizic.js App' }))` 注册了一个 service 的工厂函数。

#### App.vue

```vue
<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld :msg="foo.bar"/>
</template>

<script>
import { useService } from 'bizic-vue';
import HelloWorld from './components/HelloWorld.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
  setup() {
    // 使用 service
    const foo = useService('foo');
    return { foo };
  },
};
</script>
```

通过 `useService('foo');`，在组件中可以使用 service。

#### 完整示例
[ bizic 在线示例](https://codesandbox.io/s/github/bizic/examples/tree/master/packages/vue3-router-reactivity)

### **Vue 2.x**

?> TODO

<!-- tabs:end -->

