---
title: Vue 学习 事件修饰符
date: 2020-11-01 17:23:23
tags:
- vue
- 前端 
categories: vue 学习
---
在事件处理程序中调用 event.preventDefault() 或 event.stopPropagation() 是非常常见的需求。尽管我们可以在方法中轻松实现这点，但更好的方式是：方法只有纯粹的数据逻辑，而不是去处理 DOM 事件细节。

为了解决这个问题，Vue.js 为 v-on 提供了**事件修饰符**。之前提过，修饰符是由点开头的指令后缀来表示的。

* .stop
* .prevent
* .capture
* .self
* .once
* .passive

<!-- more -->

``` html
  <!-- 阻止单击事件继续传播 -->
  <a v-on:click.stop="doThis"></a>

  <!-- 提交事件不再重载页面 -->
  <form v-on:submit.prevent="onSubmit"></form>

  <!-- 修饰符可以串联 -->
  <a v-on:click.stop.prevent="doThat"></a>

  <!-- 只有修饰符 -->
  <form v-on:submit.prevent></form>

  <!-- 添加事件监听器时使用事件捕获模式 -->
  <!-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 -->
  <div v-on:click.capture="doThis">...</div>

  <!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
  <!-- 即事件不是从内部元素触发的 -->
  <div v-on:click.self="doThat">...</div>
```

> 使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。因此，用 v-on:click.prevent.self 会阻止**所有**的点击，而 v-on:click.self.prevent 只会阻止对元素自身的点击。

``` html
  <!-- 点击事件将只会触发一次 -->
  <a v-on:click.once="doThis"></a>
```

> 不像其它只能对原生的 DOM 事件起作用的修饰符，.once 修饰符还能被用到自定义的组件事件上。

Vue 还对应 addEventListener 中的 passive 选项提供了 .passive 修饰符。

``` html
  <!-- 滚动事件的默认行为 (即滚动行为) 将会立即触发 -->
  <!-- 而不会等待 `onScroll` 完成  -->
  <!-- 这其中包含 `event.preventDefault()` 的情况 -->
  <div v-on:scroll.passive="onScroll">...</div>
```

这个 .passive 修饰符尤其能够提升移动端的性能。
> 不要把 .passive 和 .prevent 一起使用，因为 .prevent 将会被忽略，同时浏览器可能会向你展示一个警告。请记住，.passive 会告诉浏览器你不想阻止事件的默认行为。
