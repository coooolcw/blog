使用angular和ngx-echarts的组合时遇到了严重的性能问题  
https://segmentfault.com/a/1190000012084251

调查发现ngx-echarts内部有正常使用runoutofangular来进行echarts的调用  
有可能是因为echarts实例过多引起的卡顿  

在绑定window上的resize后并没有在页面卸载后解除绑定,  
因此导致后台长期贮存,原因可能是angular的包装插件也可能是echarts本身就如此  
  
由此,在使用操作DOM为主的插件时,必须注意卸载绑定的事件    
