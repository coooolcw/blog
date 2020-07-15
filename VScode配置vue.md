目标:prettier,eslint,vuter同时运行  
  
整体结构:  
1.npm安装的eslint与prettier在本地提供shell以及保存运行  
2.vscode的插件读取本地的配置在编辑代码时手动根据配置优先级运行  
  
  
**但是vue-cli4在创建项目时会不创建prettier配置文件而是直接创建eslint的配置文件,这会导致vscode的prettier插件无法读取到正确配置**  
导致的结果就是总是有eslint提示错误  
  
项目代码风格和规范总体配置:  
1.创建项目时选择eslint+prettier  
2.设置vscode插件vuter中的各项为prettier  
3.创建.prettierrc.js并且配置,[这里参考地址](https://prettier.io/docs/en/configuration.html)  

