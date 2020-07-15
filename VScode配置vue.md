目标:prettier,eslint,vuter同时运行  
  
1.vscode与webpack的eslint不同,vscode内主要用于显示,根本还是在项目内的依赖  
[参考](https://www.imooc.com/wenda/detail/409298)  
[参考](https://segmentfault.com/q/1010000015852118)  
2.vscode的eslint用于将项目内安装的eslint配置提示或格式化到ide  
**但是vue-cli4在创建项目时会不创建prettier配置文件而是直接创建eslint的配置文件,这会导致vscode的prettier插件无法读取到正确配置**  
