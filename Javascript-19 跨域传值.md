# lesson-19 跨域传值

同源策略

![mark](http://qiniu.wind-zhou.com/blog/210313/ImbhhDD1H0.png?imageslim)

微信登录微博（第三方登录）。

![mark](http://qiniu.wind-zhou.com/blog/210313/ADH19Gi6Kb.png?imageslim)



ajax不能跨域

**利用src属性可以跨域的特点。**

jsinp:



![mark](http://qiniu.wind-zhou.com/blog/210313/E26K7eFB6C.png?imageslim)





![mark](http://qiniu.wind-zhou.com/blog/210313/A6jB0h7eB4.png?imageslim)





**jqueryde jsonp**

![mark](http://qiniu.wind-zhou.com/blog/210313/h7LFjJgjiB.png?imageslim)



​	

![mark](http://qiniu.wind-zhou.com/blog/210313/F75kDgHFfI.png?imageslim)



jasonp存在的问题：只支持get方法

因为需要传输的路径，网址等，所以用的仅是get

**跨域资源共享**

![mark](http://qiniu.wind-zhou.com/blog/210313/B6Ca2EhKgL.png?imageslim)



2.CORS（跨域资源共享）
CORS是一 个W3C标准， 全称是"跨域资源共享" (Cross origin resource sharing) 。它允许浏览器向跨源(协议+域名+端口)服务器，发出XMLHtpRequest请求，从而克服了AJAX只能同源使用的限制。
CORS需要浏览器和服务器同时支持。它的通信过程，都是浏览器自动完成，不需要用户参与。对于开发者来说，CORS通信与同源的AJAX通信没有差别，代码完全样。浏览器 旦发现AJAX请求跨源，就会自动添加一些附加的头信息，有时还会多出一 次附加的请求，但用户不会有感觉。
因此，实现CORS通信的关键是服务器。只要服务器实现了CORS接口，就可以跨源通信。





![mark](http://qiniu.wind-zhou.com/blog/210313/f32B0m6cBC.png?imageslim)





![mark](http://qiniu.wind-zhou.com/blog/210313/cDI0bj6cEA.png?imageslim)



![mark](http://qiniu.wind-zhou.com/blog/210313/fGlABc340e.png?imageslim)



这个过程中用户只需写一个ajax

**非简单请求用的不多。**

![mark](http://qiniu.wind-zhou.com/blog/210313/5dJ7ddIc3c.png?imageslim)



![mark](http://qiniu.wind-zhou.com/blog/210313/H5kDfCG27m.png?imageslim)



![mark](http://qiniu.wind-zhou.com/blog/210313/27cf8A1DBB.png?imageslim)

![mark](http://qiniu.wind-zhou.com/blog/210313/aDBEi6Be6d.png?imageslim)





跨域的一些实例：

例如第三方登录、页面的的百度地图插件，查快递等。



微信小程序并不是跨域，他是模拟了一下浏览器的环境。



跨域时，是由浏览器判断的，如果是跨域，则会添加一个origin字段。

