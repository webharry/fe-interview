## HTML5 概念

HTML5 是一种用于创建 Web 页面的新一代标准，它带来了许多新的特性和改进。

### HTML5 有什么新特性？
##### 1.语义化标签：

HTML5 引入了许多语义化标签，如 ```<header>、<footer>、<nav>、<article>、<section>``` 等，这些标签可以让页面结构更清晰，便于阅读和维护。

##### 2.表单控件：

HTML5 引入了一些新的表单控件，如日期选择器、颜色选择器、搜索框、范围选择器等，可以使表单更加易于使用和定制。

##### 3.视频和音频支持
HTML5 支持直接在网页中嵌入视频和音频，不再需要使用第三方插件，如 Flash。

##### 4.Canvas 绘图

HTML5 引入了 Canvas 元素，可以使用 JavaScript 绘制图形和动画，实现更加丰富的网页效果。

##### 5.SVG 图形支持

HTML5 支持直接在网页中使用 SVG（可缩放矢量图形），可以实现高质量的图形和动画效果。

##### 6.Web Workers

HTML5 引入了 Web Workers，可以在后台运行 JavaScript 代码，提高页面的性能和响应速度。

##### 7.Geolocation

HTML5 支持通过浏览器获取用户的地理位置信息，可以实现一些基于位置的应用和服务。

##### 8.Web Storage

Web Storage 是 HTML5 新增的一种浏览器存储机制，它可以在客户端存储数据而无需像 Cookie 那样发送到服务器端。有两种类型：本地存储（localStorage）和会话存储（sessionStorage）。

### HTML5 新特性的高频考点
**面试官：说说浏览器存储机制及 localStorage、sessionStorage、Cookie 三者的异同点？**

(1).localStorage：是一种持久化的存储机制，可以用于长期存储网站的数据。localStorage 存储的数据不会过期，除非手动删除或者用户清空浏览器缓存。可以使用 JavaScript 的 localStorage 对象来访问和操作 localStorage。

(2).sessionStorage：是一种会话级别的存储机制，数据只在当前会话有效。如果用户关闭了浏览器窗口或标签页，存储的数据将会丢失。可以使用 JavaScript 的 sessionStorage 对象来访问和操作 sessionStorage。

(3).Web Storage 的优点：
① 存储容量大：Web Storage 的存储容量比 Cookie 大得多，通常可以存储几十兆的数据。Cookie 存储量不能超过 4KB。

② 速度快：Web Storage 的读写速度比 Cookie 快，因为 Web Storage 是基于浏览器端的本地存储，不需要像 Cookie 一样发送到服务器端。

③ 更安全：Web Storage 存储的数据不会被发送到服务器端，因此不会被网络攻击者窃取

##### (4).Web Storage 的应用场景：
① 缓存数据：可以将一些静态数据缓存在 localStorage 中，减少每次请求数据的开销，提高网站性能。

② 用户偏好设置：可以将用户的偏好设置存储在 localStorage 中，下次用户访问网站时可以自动加载。

③ 登录状态保存：可以使用 localStorage 存储用户的登录状态，避免用户每次访问网站都需要重新登录。

需要注意的是，Web Storage 是基于域名的，不同域名之间的 Web Storage 不能共享数据，同一个域名下的不同页面可以共享 Web Storage 。另外，Web Storage 存储的数据是明文存储的，需要注意安全问题。

## 结论
* 1.HTML 的主要作用是将信息呈现在网页上，为网页内容提供结构和语义化，使得网页内容更加易于理解和处理。通过使用不同的 HTML 标签，可以实现不同的效果。
* 2.HTML语义化是一种在创建HTML页面时使用正确的标记来正确地描述内容的含义和结构的做法。它有助于提高页面的可访问性、可维护性和可读性，并且有助于提高页面的排名和流量。在实践中，我们可以使用语义化标记、避免使用无语义的标记，使用标题标记、列表标记、表格标记、段落标记和语义化的图片标记来实现HTML语义化。
* 3.HTML5 引入了一些新功能，如语义元素、多媒体元素、表单控件、本地存储、离线应用程序等。它还引入了新的API，如Canvas API、Web Workers API、Web Sockets API等，以及改进了现有的API。


## 📢 update 同步更新
[掘金专栏](https://juejin.cn/column/7218749269896970299) | [知乎专栏](https://www.zhihu.com/column/c_1627260575263817728) | [Github](https://github.com/webharry/fe-interview) | [简书专栏](https://www.jianshu.com/c/8ee0e31d826e) | [CSDN](https://blog.csdn.net/web_harry) | [segmentfault](https://segmentfault.com/u/yangjie_5f0c1f890b88a/articles)

## ❗️转载声明
- 声明
可以转载里面的所有面试题用到任何地方，但请添加仓库的地址:https://github.com/webharry/fe-interview，因为转载后你们很少会更新了，但此仓库每周都会准时更新。

©️ License
[MIT License](https://github.com/webharry/fe-interview/blob/master/LICENSE)
Copyright 2023 webhary
