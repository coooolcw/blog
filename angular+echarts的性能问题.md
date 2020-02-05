使用angular和ngx-echarts的组合时遇到了严重的性能问题  
https://segmentfault.com/a/1190000012084251

调查发现ngx-echarts内部有正常使用runoutofangular来进行echarts的调用  
有可能是因为echarts实例过多引起的卡顿  
在项目中使用了30个echarts的实例  
但是echarts在实例页面卸载以后仍然在调用也还是事实  
