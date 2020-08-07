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
  
  
  组件是可复用的vue实例,每个组件都是一个new vue(),[不是很完善的参考文章](https://segmentfault.com/a/1190000020781076)  
    
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
  6.非prop的attribute(不常用,主要用于编写基础组件,调整未设置的传入的props的接收位置),使用的时候注意class和style会合并,其他属性会覆盖  
    使用`inheritAttrs: false`禁止外部修改组件的根元素.禁止的同时可以使用实例的`$attrs`属性获取传入的未接收属性,可分配到组件内需要分配的地方  
  
  三.自定义事件(编写基础组件库常用)  
  ---
  **vue的事件监听分为两种,原生DOM结构可以监听原生事件,例如click,mouseenter等等  
  而在组件上监听的都是自定义事件,必须在其他地方emit才能触发  
  也就是说在组件上监听click是监听不到内部的click事件的冒泡和捕获,无法被触发的.  
  如果想监听子组件内部的click而不在子组件内部的click事件进行emit的话,需要在事件上添加native后缀  
  这样就能变成在组件的根元素上监听原生事件,也就可以进行在冒泡和捕获阶段接收到原生事件**  
  
  
  1.事件名不存在自动大小写转换,使用kebab-case事件名  
  2.自定义v-model使用vue对象的model选项,实际就是把一个event事件的传参和prop的值绑定  
  3.$listeners用于修改在调用组件时绑定在根元素的事件,可获取除native以外的全部监听事件  
  4.在模板DOM结构上监听原生事件(例如click)不需要emit触发,反之则需要emit触发自定义事件  
  5.`.sync`是在父组件上自动绑定'update:myPropName'事件监听的语法糖,在子组件需要触发emit,父组件会自动接收传上来的数据  
  **实际使用双向绑定时推荐使用sync,以增加可读性与可维护性**,[参考](https://medium.com/%E4%B8%80%E5%80%8B%E5%B0%8F%E5%B0%8F%E5%B7%A5%E7%A8%8B%E5%B8%AB%E7%9A%84%E9%9A%A8%E6%89%8B%E7%AD%86%E8%A8%98/vue-%E4%BD%BF%E7%94%A8-props-async-%E5%90%8C%E6%AD%A5%E7%88%B6%E5%AD%90%E7%B5%84%E5%BB%BA%E4%B9%8B%E9%96%93%E7%9A%84%E5%82%B3%E5%80%BC-f7b1d3007836)  
  
  四.插槽
  ---
  1.作用域规则:父级模板里的所有内容都是在父级作用域中编译的;子模板里的所有内容都是在子作用域中编译的.  
  2.不带name属性的插槽默认名default  
  3.v-slot:slot-name只能添加在template上  
  4.插槽prop只在父元素的插槽内容中可用,尽量不要使用独占默认插槽的缩写,使用完整的template插槽语法  
  
  五.动态组件,异步组件  
  ---
  1.`<keep-alive>`本身不会被渲染,并且可以[控制缓存规则](https://cn.vuejs.org/v2/api/#keep-alive)  
  2.在.vue文件中注册的组件可以使用import进行异步导入,vue-router中也可以(有自动示例)  
  
  
  
  六.其他
  ---
  1.`$root`与`$parent`不要多用  
  2.`$refs`只会在组件渲染完成之后生效,并且它们不是响应式的.优先在M层操作而不是去操作refs  
  3.依赖注入类似于大范围的props属性下发,同样不推荐大规模使用  
  4.Vue 的事件系统不同于浏览器的 EventTarget API.尽管它们工作起来是相似的,  
  但是 $emit,$on,和 $off 并不是 dispatchEvent,addEventListener 和 removeEventListener 的别名  
  5.组件可以递归和循环调用,但是要注意无限循环  
  


N.UI组件库相关  
===  
  
  element-ui更新频率大幅度降低,并没有随着vue3.0的发布而有起色,可以预见将会和mintui一样淡出  
  现在推荐vuetify,iview(据说bug有点多),
  
