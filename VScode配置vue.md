目标:prettier,eslint,vuter同时运行  
  
1.vscode与webpack的eslint不同,配置也需要多重考虑  
[参考](https://www.imooc.com/wenda/detail/409298)  
[参考](https://segmentfault.com/q/1010000015852118)  
2.vscode的eslint用于将项目内安装的eslint配置提示或格式化到ide,不会在shell内跑,但是结果是一样的  
3.prettier可以类似eslint的使用方法(两边都安装),也可以只在vscode安装  
vue初始化项目可使用"eslint-plugin-prettier"来协调eslint与prettier,初始化时选择此项目,在项目内也会自动安装  
4.在.eslintrc.js文件中需要有
