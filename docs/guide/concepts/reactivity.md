# Reactivity

上一部分，我们罗列了 service 部分的功能，在实际使用中，一些 service 的数据可能需要是响应式的，以便驱动视图更新，因此对于响应式的数据，需要使用 `Reactivity` 模块；

bizic 提供了 `Reactivity` 的统一 api 标准，但不同框架需要使用不同的库，比如在 Vue 中，我们需要使用 `bizic-reactivity-vue`，该模块基于 vue 的`@vue/reactivity` 进行了封装，提供了响应式数据的能力；

## 安装
通过 npm 安装
<!-- tabs:start -->

### **Vue 3.x**

```shell
npm i bizic-reactivity-vue
```
### **Vue 2.x**

?> TODO

<!-- tabs:end -->

## 创建一个响应式数据

可以通过以下方式创建一个响应式的数据：
  - `observable(obj)`：创建一个响应式代理数据；
  - `shallowObservable(obj)`：创建一个响应式代理数据，它跟踪其自身 property 的响应性，但不执行嵌套对象的深层响应式转换。

### observable(obj)
创建一个响应式的数据
```js
import { observable } from 'bizic-reactivity-vue';

const observed = observable({ name: 'bizic', foo: { bar: 'fooo' } });
observed.name = 'bizic-reactivity'; // 数据是响应式的
observed.foo.bar = 'foooo'; // 数据是响应式的
```

### shallowObservable(obj)
创建一个响应式代理数据，只跟踪其自身 property 的响应性。
```js
import { shallowObservable } from 'bizic-reactivity-vue';

const observed = shallowObservable({ name: 'bizic', foo: { bar: 'fooo' } });
observed.name = 'bizic-reactivity'; // 数据是响应式的
observed.foo.bar = 'foooo'; // 数据不是响应式的
```
## 创建一个响应式的 Service
 
除了通过以上方式将一个普通 Service 转化成 响应式的 Service，还可以通过继承 `Observable` 和 `ShallowObservable` 来实现。

### Observable

```js
import { Observable } from 'bizic-reactivity-vue';

export default class FooStoreService extends Observable {
  foo = 'Hi'; // 响应式的数据

  get bar() { // computed
    return `${this.foo} bizic!`;
  }

  updateFoo(foo) {
    this.foo = foo;
  }
}
```
其中属性 `foo` 是响应式的，属性 `bar` 会转化成一个`memoized getter`，`bar` 的值会被缓存起来，只有 `foo` 发生变化时，`bar` 才会被重新计算。

### ShallowObservable

同 `Observable`，不同的是只跟踪其自身 property 的响应性。