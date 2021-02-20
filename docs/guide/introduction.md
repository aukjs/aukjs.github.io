# 介绍

## Bizic.js 是什么

bizic.js（business logic 的缩写）是一个基于DI的轻量级前端框架，专注于业务逻辑。解构视图逻辑和业务了逻辑，为你的项目逻辑组织提供更有力的支撑。

## 示例

<!-- tabs:start -->
### **Vue 3.x**

####  main.js
[main.js](https://raw.githubusercontent.com/bizic/examples/master/packages/vue3-simple/src/main.js ':include :type=code')

我们通过 `bizic.registerServiceFactory('foo', () => ({ bar: 'Welcome to Your Bizic.js App' }))` 注册了一个 service 的工厂函数。

#### App.vue
[App.vue](https://raw.githubusercontent.com/bizic/examples/master/packages/vue3-simple/src/App.vue ':include :type=code')

通过 `useService('foo');`，在组件中可以使用 service。

#### 完整示例
[ bizic 在线示例](https://codesandbox.io/s/github/bizic/examples/tree/master/packages/vue3-simple)

### **Vue 2.x**

 ?> TODO

<!-- tabs:end -->

## 设计动机

### 前端代码的组织方式
