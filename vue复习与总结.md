一.vue实例  
===
  
二.模板语法  
===
  




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
    
二.class与style
===  
  暂时没有需要提的.  
  [主要参考官方文档](https://cn.vuejs.org/v2/guide/class-and-style.html)  
  
    
  
  
  
