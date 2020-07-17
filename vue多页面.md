1.vue-cli的多页面配置较为简单,在vue.config.js中配置即可  
我自己的项目配置,三个页面  
```js
const path = require("path");

function resolve(dir) {
  return path.join(__dirname, dir);
}

module.exports = {
  pages: {
    index: {
      entry: "src/pages/index/indexMain.js",
      title: "目录",
    },
    windows: {
      entry: "src/pages/windows/windowsMain.js",
      title: "仿windows",
    },
    nisuwa: {
      entry: "src/pages/nisuwa/nisuwaMain.js",
      title: "nisuwa官方网站",
    },
  }
};
```
