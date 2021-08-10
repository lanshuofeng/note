BOM是浏览器对象模型(Browser Object Model )

### 1. `window`
1. `window`对象是BOM的核心， 是`Global对象`， 所有`var`的全局变量和函数都是`window`的属性，而`let/const`则不行

2. 打开新窗口
`window.open(url, '_blank|self', params...)`
- 为防止恶意弹窗，浏览器一般禁止在网页加载的过程中通过`window.open`的方式打开新页面，会提示`弹窗被拦截`
- 打开新窗口还可以不采用`window.open`的方式， 某些不良网站打开一次会发生多次跳转

### 2. `location`
`location`对象包含当前页面的`url`的`host, hostname, port, username, password`等信息，  `location`也可以实现页面跳转:

- `location.assgin('http://123.com')`
- `window.location = 'http://123.com'`
- `location.href = 'http://123.com'`

这三种跳转是等价的, 跳转之后浏览器会增加一条历史记录，并且可以根据“回退”按钮返回上一级

---

- `location.replace('http://123.com')` 

这种跳转不会添加新的历史记录，无法通过“回退”按钮回到原来的地址。某些不良网站就可以通过多次使用`setTimeout(window.replace('http://xxx.com'), 2000,'')`的方式层层跳转到最终的目的地址

---

- `location.reload() //刷新页面(会有缓存)`
- `location.reload(true) //  强制不走缓存重新加载页面`

这两种是刷新页面，在某些修改操作执行完成之后需要重新加载页面


### 3. `navigator`
`navigator`有很多属性，能获取当前浏览器的名称， 版本，语言偏好，以及插件等信息。某视频网站能检测到用户安装了防广告插件并强制用户必须等待
```javascript
//  获取app名称
> window.navigator.appName
< "Netscape"

//  获取app版本
> window.nagivator.appVersion
< "5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.164 Safari/537.36 Edg/91.0.864.71"

// 获取浏览器插件的个数， 可遍历插件判断是否安装了某插件。如果是IE浏览器需要特殊处理
> window.navigator.plugins.length
< 3

```

### 4.  `hostory`
>用户每次点击都会触发页面刷新的 时代早已过去，“后退”和“前进”按钮对用户来说就代表“帮我切换一个状态”的历史也就随之结束了                                                                      
—— *<<JavaScript高级程序设计（第4版）>>*

`history`对象管理浏览器的历史记录，对外不会暴露明细的`url`,  但是会暴露`length`，并且提供`back()`, `forward()`, `go(1)`, `go(-1)`这样的方法返回到历史状态，这些历史状态不会重新请求服务端， 而是浏览器缓存了页面的数据。因此即使在离线状态下浏览器依然可以“前进”和“后退”




