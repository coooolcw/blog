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



N.组件相关
===
  一.在ul>li,table>tr,select>option之类的嵌套元素组合中,使用子组件需要这样
  ```Vue.js
  <ul>
    <li
      is="todo-item"
      v-for="(todo, index) in todos"
      v-bind:key="todo.id"
      v-bind:title="todo.title"
    ></li>
  </ul>
  ```
  这样做实现的效果与<todo-item>相同,但是可以避开一些潜在的浏览器解析错误.
  [参考](https://cn.vuejs.org/v2/guide/components.html#%E8%A7%A3%E6%9E%90-DOM-%E6%A8%A1%E6%9D%BF%E6%97%B6%E7%9A%84%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9)  
  

