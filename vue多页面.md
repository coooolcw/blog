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
2.跳转问题  
devserver.  
默认打开index.html,无法和线上一样通过域名跳转  
可行的方法:  
```HTML
<a href="windows.html">link to windows page</a>
<a href="corp.html">link to corp page</a>
```
这样可以直接跳转到html,同时不会被router影响  
但是无法在线上跳转域名    
nginx.  
线上需要配置nginx跳转  
