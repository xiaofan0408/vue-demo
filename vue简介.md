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
#### v-bind

#### v-model

### 过滤器

### 自定义指令

### 计算属性和侦听器

### 组件

### 路由

### 状态管理

