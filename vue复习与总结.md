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
  
三.条件渲染与列表渲染  
===
  1.v-else与v-else-if必须跟在v-if或者v-else的后面,否则无法识别  
  2.key管理可复用元素,有相同父元素的子元素必须有独特的key,除非子元素设计为重复使用  
  3.v-if与v-show的渲染机制不同,v-show用于频繁切换,v-if为惰性的,类似于计算属性

四.key  
===
  key管理可复用元素,有相同父元素的子元素必须有独特的key,除非子元素设计为重复使用  
  建议尽可能在使用v-for时提供key attribute,除非遍历输出的DOM内容非常简单,或者是刻意依赖默认行为以获取性能上的提升.  
  key的特殊attribute主要用在Vue的虚拟DOM算法,在新旧nodes对比时辨识VNodes  
  [官方文档](https://cn.vuejs.org/v2/api/#key)  
  [具体解释](https://www.jianshu.com/p/4bd5e745ce95)  
  [深度参考1](https://github.com/sl1673495/blogs/issues/39)  
  [深度参考2-diff](https://juejin.im/post/5e7c680451882535e2042bc9)  
  **注意:不要使用数组的index作为key**  
  同时不要使用随机数作为key  
