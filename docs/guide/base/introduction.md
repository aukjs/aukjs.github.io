# 介绍

## Bizic.js 是什么

bizic.js（business logic 的缩写）是一个基于 DI (Dependency Injection，依赖注入)的轻量级前端应用框架，专注于业务。

bizic 抽象了 service 的概念，通过将业务逻辑和一些其他非视图逻辑抽离到 service 中，可以很好的解耦视图逻辑和业务逻辑，为实现一个清晰可控的业务架构提供有力的支撑。

一个使用了 bizic 的应用可以简化如下所示：

![Provider Tree](_media/service.drawio.svg ':class=img-center')

当然，bizic 的功能远不止于此，跟多的功能请看后续文档。

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

