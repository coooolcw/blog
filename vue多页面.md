1.vue-cli的多页面配置较为简单,在vue.config.js中配置即可  
我自己的项目配置,三个页面  
```js
module.exports = {
  pages: {
    // 多页面配置
    index: {
      entry: "src/pages/index/entry.js",
      title: "目录",
      template: "src/pages/index/index.html",
    },
    windows: {
      entry: "src/pages/windows/entry.js",
      title: "仿windows",
      template: "src/pages/windows/windows.html",
    },
    corp: {
      entry: "src/pages/corp/entry.js",
      title: "nisuwa官方网站",
      template: "src/pages/corp/corp.html",
    },
  },
};
```
2.build打包以后在nginx中配置后可以正常使用,但是开发的devserver无法正常进行跳转  
需要配置webpack  
