目标:prettier,eslint,vuter同时运行  
  
1.vscode与webpack的eslint不同,vscode内主要用于显示,根本还是在项目内的依赖  
[参考](https://www.imooc.com/wenda/detail/409298)  
[参考](https://segmentfault.com/q/1010000015852118)  
2.vscode的eslint用于将项目内安装的eslint配置提示或格式化到ide  

vue-cli4有问题,正在研究
1.eslint-config-prettier 是最新的解决eslint与prettier冲突的组件  
```shell
npm install --save-dev eslint-config-prettier
```
安装后需要在.eslintlrc.js中添加
```
extends: [
"prettier",
"prettier/vue"
]
```
在extends的最后  
但是无法解决vuter在vue文件中js部分的冲突,正在研究  
