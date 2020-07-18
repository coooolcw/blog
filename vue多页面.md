1.vue-cli的多页面配置较为简单,在vue.config.js中配置即可  
我自己的项目配置,三个页面  
```js
module.exports = {
  pages: {
    // 多页面配置
    index: {
      entry: "src/pages/index/entry.js",
      title: "目录",
    },
    windows: {
      entry: "src/pages/windows/entry.js",
      title: "仿windows",
    },
    corp: {
      entry: "src/pages/corp/entry.js",
      title: "nisuwa官方网站",
    },
  },
};
```
