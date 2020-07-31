一.计算属性和侦听器  
===
  一.计算属性与方法以及侦听器的区别  
  ---  
    
  [文档](https://cn.vuejs.org/v2/guide/computed.html)  
  1.methods与computed相比没有缓存功能  
  2.watch与computed相比书写冗余,功能类似  
    
  二.计算属性可以另行设置setter  
  ---  
  
  三.computed与watch的使用时机区别
  ---
  1.有异步时使用watch,computed不支持异步  
  2.多个数据影响一个数据用computed,一个数据改变影响多个数据使用watch  
  3.内部逻辑复杂操作多的使用watch  
  4.computed在初始化时会执行一次,watch不会  
  5.watch还有其他参数可供选择,包括deep,immediate,同时可以传入数组,[详情](https://cn.vuejs.org/v2/api/#watch)  
  
二.Class 与 Style 绑定  
===  
  
  在实际开发中,常使用的是将class属性绑定一个返回对象的**计算属性**.  
  实际业务开发中,除了使用UI组件库时,不常使用style系语法,主要关注class语法  
  
三.条件渲染  
===
  1.v-else与v-else-if必须跟在v-if或者v-else的后面,否则无法识别  
  2.key管理可复用元素,有相同父元素的子元素必须有独特的key,除非子元素设计为重复使用  
  3.v-if与v-show的渲染机制不同,v-show用于频繁切换,v-if为惰性的,类似于计算属性  
  
四.列表渲染
===
  一.数组中推荐使用for of,而不是for in  
  ---  
  
  二.数据的监听  
  ---  
    
  1.数组改变可以被监听的方法有限  
  2.数组替换可以被监听到,如filter,concat,**slice**,也可以直接替换数组  
  
  三.对象的监听  
  ---  
    
  1.对象使用for in  
  2.在遍历对象时，会按Object.keys()的结果遍历,但是顺序不能保证
    
  四.template的作用
  ---
    
  可以包裹元素,但是不会被渲染在页面上  
  常用于包裹多个同数组循环  
  ```Vue.js
  <template v-for="(item, index) of list" :key="item.id">
    <div>{{item.something}}</div>
    <div>{{item.otherthing}}</div>
  </template>  
  ```
    
  五.可以使用计算属性或方法返回修改后的数组来保持原始数据不变  
  ---
  六.一般不要把v-if和v-for在一个元素上使用  
  ---
  实际在实现中v-for优先于v-if  
  但是如果只想渲染部分节点,可以这么做  
  ```
  <li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo }}
  </li>
  ```

五.key  
===
  key管理可复用元素,有相同父元素的子元素必须有独特的key,除非子元素设计为重复使用  
  建议尽可能在使用v-for时提供key attribute,除非遍历输出的DOM内容非常简单,或者是刻意依赖默认行为以获取性能上的提升.  
  key的特殊attribute主要用在Vue的虚拟DOM算法,在新旧nodes对比时辨识VNodes  
  [官方文档](https://cn.vuejs.org/v2/api/#key)  
  [具体解释](https://www.jianshu.com/p/4bd5e745ce95)  
  [深度参考1](https://github.com/sl1673495/blogs/issues/39)  
  [深度参考2-diff](https://juejin.im/post/5e7c680451882535e2042bc9)  
  **注意:不要使用数组的index作为key**  
  **不要使用随机数作为key**  
  **不要使用对象或数组之类的非基本类型值作为v-for的key,用字符串或数值类型的值.**  

六.事件  
===  
  修饰符产生的代码会以顺序执行,如self判断失败后后续的修饰符也不会有效  
  事件修饰符中的self实际为:e.target = e.currentTarget才进入下一步  
  ```
  使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。  
  因此，用 v-on:click.prevent.self 会阻止所有的点击，而 v-on:click.self.prevent 只会阻止对元素自身的点击。  
  ```
  [解释](https://www.oschina.net/question/1785591_2273843?sort=default)  
  
七.输入绑定  
===
```
v-model 会忽略所有表单元素的 value、checked、selected attribute 的初始值而总是将 Vue 实例的数据作为数据来源。
```
```
如果 v-model 表达式的初始值未能匹配任何选项，<select> 元素将被渲染为“未选中”状态。
在 iOS 中，这会使用户无法选择第一个选项。因为这样的情况下，iOS 不会触发 change 事件。
因此，更推荐像上面这样提供一个值为空的禁用选项。
```

八.组件  
===
  
  一.组件注册
  ---
  1.局部注册的组件在其子组件中不可用  
  2.基础组件全局注册使用require.context(),[参考](https://webpack.docschina.org/guides/dependency-management/#requirecontext)  
  不太常用,一般基础组件会打包成插件然后调用vue.use()[插件参考](https://cn.vuejs.org/v2/guide/plugins.html)  
    
  二.prop
  ---
  1.传入数据不带v-bind(或者缩略符`:`)全部为字符串,带v-bind为js表达式  
  2.v-bind不带参数传(取代v-bind:prop-name="...")可直接将对象整个传入  
  3.在JavaScript中对象和数组是通过引用传入的,所以对于一个数组或对象类型的prop来说,在子组件中改变变更这个对象或数组本身将会影响到父组件的状态.  
  4.prop验证,default值如果是对象/数组,必须用函数返回  
  5.prop类型检查支持自定义构造函数  


N.UI组件库相关  
===  
  
  element-ui更新频率大幅度降低,并没有随着vue3.0的发布而有起色,可以预见将会和mintui一样消逝  
  
