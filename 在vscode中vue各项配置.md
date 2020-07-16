一.目标:prettier,eslint,vuter同时运行  
  
整体结构:  
1.npm安装的eslint与prettier在本地提供shell以及保存运行  
2.vscode的插件读取本地的配置在编辑代码时手动根据配置优先级运行  
  
  
**但是vue-cli4在创建项目时会不创建prettier配置文件而是直接创建eslint的配置文件,这会导致vscode的prettier插件无法读取到正确配置**  
导致的结果就是总是有eslint提示错误  
  
项目代码风格和规范总体配置:  
1.创建项目时选择eslint+prettier  
2.设置vscode插件vuter中的各项为prettier  
3.创建.prettierrc.js并且配置,[这里参考地址](https://prettier.io/docs/en/configuration.html)  
  
建议配置为:  
```js
module.exports = {
  trailingComma: "es5",
  semi: true,
  arrowParens: "always",
};
```
trailingComma为最后的逗号,  
semi为分号,  
arrowParens为箭头函数总是包含括号  
这是根据prettier的默认配置来覆盖vue-cli默认创建的配置  
  
二.路径自动补全和提示  
1.关闭vscode中的默认提示,不太好用  
在设置中的
```
JavaScript › Suggest: Paths
在 import 语句和 require 调用中，启用或禁用路径建议。
```
和
```
TypeScript › Suggest: Paths
在 import 语句和 require 调用中，启用或禁用路径建议。
```
安装vscode插件Path Intellisense  
安装说明中就有关闭vs原生补全的说明  
然后在项目根目录创建jsconfig.json  
内部输入  
```json
{
  "allowJs": true,
  "compilerOptions": {
    "baseUrl": "./",
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```
