## Vue 简介

### Vue 实例
```bash
var vm = new Vue({
  el: '#example',
  data: data,
  methods: {
      test: function(){
      }
  },
  created: function () {
    console.log('a is: ' + this.a)
  }
})
```
可以访问创建的vue实例里面的实例数据
```bash
vm.$data 
vm.$el
vm.$watch('a', function (newValue, oldValue) {
})
```
[vue的实例变量](https://cn.vuejs.org/v2/api/#%E5%AE%9E%E4%BE%8B%E5%B1%9E%E6%80%A7)

### 生命周期

![vue生命周期图示](https://cn.vuejs.org/images/lifecycle.png)

[vue的完整生命周期](https://cn.vuejs.org/v2/api/#%E9%80%89%E9%A1%B9-%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E9%92%A9%E5%AD%90)

实现一个生命周期钩子的示例
```bash
 created: function () {
    // `this` 指向 vm 实例
    console.log('a is: ' + this.a)
 }
```

### 模板语法

#### 插值 

```bash
{{ data}}
```
data 可以是实例中数据对象里面的变量也可以是javascript的表达式, 表达式如下所示
```bash
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}
```
插值里面只能是js表达式不能是语句
#### v-html
一般插值会将输出的内容当作字符串，如果想输出html就需要使用v-html指令
```bash
<p>Using v-html directive: <span v-html="rawHtml"></span></p>
```
#### v-if
在vue中我们可以使用v-if去实现一个条件块，示例如下：
```bash
<h1 v-if="ok">Yes</h1>
```
当v-if的表达式的值为true的时候，就会在页面上显示这些HTML代码
vue提供了v-else 来实现条件块的另一个分支选择，在vue2.1.0版本后添加了 v-else-if 来实现多分支语句，一个完整的示例如下：
```bash
div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```
#### v-show
v-show 与v-if 类似同样是用来实现条件块的，只是没有另外的分支，最主要的区别是 当v-if的表达式为false时是没有渲染的，而v-show是有渲染的，为false时只是通过css的样式display:none去
隐藏显示，示例如下：
```bash
<h1 v-show="ok">Hello!</h1>

```

#### v-for
当需要显示一个数组的时候就可以使用v-for去渲染显示，使用 item in items 形式的特殊语法，items 是源数据数组并且 item 是数组元素迭代的别名。要获取数组中元素的下标可以使用 (item, index) in items 去获取，示例如下:
```bash
  <li v-for="item in items">
    {{ item.message }}
  </li>
```
详细信息可以看 [v-for的官方教程](https://cn.vuejs.org/v2/guide/list.html)
#### v-bind
通过v-bind 可以为一个标签的属性或者组件的属性绑定一个变量或者值，绑定组件的属性必须在组件的props中声明，v-bind可以缩写成：，为单向绑定，示例如下
```bash
<!-- 绑定一个属性 -->
<img v-bind:src="imageSrc">

<!-- 缩写 -->
<img :src="imageSrc">

<!-- 内联字符串拼接 -->
<img :src="'/path/to/images/' + fileName">

<!-- class 绑定 -->
<div :class="{ red: isRed }"></div>
<div :class="[classA, classB]"></div>
<div :class="[classA, { classB: isB, classC: isC }]">

<!-- style 绑定 -->
<div :style="{ fontSize: size + 'px' }"></div>
<div :style="[styleObjectA, styleObjectB]"></div>

<!-- 绑定一个有属性的对象 -->
<div v-bind="{ id: someProp, 'other-attr': otherProp }"></div>

<!-- 通过 prop 修饰符绑定 DOM 属性 -->
<div v-bind:text-content.prop="text"></div>

<!-- prop 绑定。“prop”必须在 my-component 中声明。-->
<my-component :prop="someThing"></my-component>

<!-- 通过 $props 将父组件的 props 一起传给子组件 -->
<child-component v-bind="$props"></child-component>

<!-- XLink -->
<svg><a :xlink:special="foo"></a></svg>
```

#### v-model
与v-bind类似都是绑定一个变量到属性值，不同的是v-model是双向绑定同时v-model只能用在以下的控件中：
```bash
<input>
<select>
<textarea>
components
```


### 计算属性和侦听器

#### 计算属性
简单的文本转换可以通过filters来转换，但是当涉及到复杂的逻辑的时候就要通过计算属性完成了,计算属性都是以函数的形式写在computed选项中，计算属性中的this指向Vue实例本身，只要最后有返回的值就行, 示例如下：
```bash
 computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
  }
```
我们可以通过编写一个方法达到与计算属性相同的效果，不同的是计算属性是基于它们的依赖进行缓存的。计算属性只有在它的相关依赖发生改变时才会重新求值，而方法则是在每当触发重新渲染时，调用方法将总会再次执行函数。

#### 侦听器
Vue 提供了一种更通用的方式来观察和响应 Vue 实例上的数据变动：侦听属性。示例如下：
```bash
 watch: {
    firstName: function (val) {
      this.fullName = val + ' ' + this.lastName
    },
    lastName: function (val) {
      this.fullName = this.firstName + ' ' + val
    }
  }
```

### 组件

可以通过以下方式定义一个组件
```bash
Vue.component('button-counter', {
  data: function () {
    return {
      count: 0
    }
  },
  template: '<button v-on:click="count++">You clicked me {{ count }} times.</button>'
})
```
#### 通过 Prop 向子组件传递数据
Prop 是你可以在组件上注册的一些自定义特性。当一个值传递给一个 prop 特性的时候，它就变成了那个组件实例的一个属性。
```bash
Vue.component('item', {
  props: ['title'],
  template: '<h3>{{ title }}</h3>'
})
```
一个组件默认可以拥有任意数量的 prop，任何值都可以传递给任何 prop。在上述模板中，你会发现我们能够在组件实例中访问这个值，就像访问 data 中的值一样。
一个 prop 被注册之后，你就可以像这样把数据作为一个自定义特性传递进来：
```bash
<item title="My journey with Vue"></item>
<item title="Blogging with Vue"></item>
<item title="Why Vue is so fun"></item>
```

#### 通过事件向父级组件发送消息

我们可以调用内建的 $emit 方法并传入事件的名字，来向父级组件触发一个事件：

```bash
<button v-on:click="$emit('enlarge-text', 0.1)">
  Enlarge text
</button>
```
在父组件中就可以通过向子组件绑定事件去进行交互

```bash
<item
  v-on:enlarge-text="postFontSize += $event"
></item>
```
### 路由

[Vue-Router官方教程](<https://router.vuejs.org/zh-cn/>)

Vue-Router 是一个官方推荐的路由组件，vue自身并没有自带路由功能

#### 安装
```bash
npm install vue-router
```

#### 使用
如果在一个模块化工程中使用它，必须要通过 Vue.use() 明确地安装路由功能：
```bash
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter)
```
#### 路由配置
一个简单的路由配置如下所示：
```bash
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User,
      children: [
        {
          path: 'profile',
          component: UserProfile
        },
        {
          path: 'posts',
          component: UserPosts
        }
      ]
    }
  ]
})
```
#### 路由跳转

路由跳转有以下两种方式

| 声明式  | 编程式 | 
| -  | - | 
| `<router-link :to="...">` | `router.push(...)` | 


### 状态管理

[Vuex官方教程](<https://vuex.vuejs.org/zh-cn/>)

Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。Vuex 也集成到 Vue 的官方调试工具 devtools extension，提供了诸如零配置的 time-travel 调试、状态快照导入导出等高级调试功能。

#### 安装 与 使用

```bash
npm install vuex --save
```
在一个模块化的打包系统中，您必须显式地通过 Vue.use() 来注册 Vuex：
```bash
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)
```
当使用全局 script 标签引用 Vuex 时,则
```bash
<script src="/path/to/vuex.js"></script>
```
