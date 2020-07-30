一.vue-cli的多页面配置较为简单,在vue.config.js中配置即可  
自己的项目配置,三个页面  
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
这后面还可以用函数来自动化获取,另外还有chunk优化性能的部分还没有研究过  
可以留作以后的实验空间  
二.跳转问题  
1.devserver.  
vue-cli使用的webpack中的devserver默认打开index.html,  
无法和线上一样通过域名跳转,并且无法多端口代理多文件  
(可以使用多个express另外开启但是这样无法在cli中使用各种vue的服务)  
因此解决方法:  
```HTML
<a href="windows.html">link to windows page</a>
<a href="corp.html">link to corp page</a>
```
这样可以直接跳转到html,同时不会影响单个spa的route,点击任意router-link就会变成正常的localhost地址  
但是这种方法部署到线上以后,无法在线上跳转域名,无法正常使用,  
因此需要nginx进行域名跳转,将各个html页面跳转到子域名,在子域名下呈现单个spa.        
2nginx.   
首先在dns打开所有域名的匹配  
然后在/etc/nginx/sites-enabled文件夹创建nisuwa配置文件  
方法:主域名判断是否跳转,子域名自动识别域名寻找html文件,找不到会自动返回403,怎么设置返回404不清楚,时间关系不深入了  
完整配置如下  
```
server {
	listen 80;

	server_name nisuwa.com www.nisuwa.com;

	root /web/nisuwa;
	index index.html;

	location ~* (\w*).html$ {
		set $pagename $1;
		if ($pagename != "index") {
			return http://$pagename.nisuwa.com;
		}
	}
}

server {
	listen 80;

	server_name ~^(\w*).nisuwa.com$;

	set $subdomain $1;

	root /web/nisuwa;
	index $subdomain.html;

	try_files $uri $uri/ =404;
}
```

三.现有问题为子域名跳转后共用的chunk和css文件由于跨域原因不能共享缓存
===
在webpack中寻找设置,暂缓
