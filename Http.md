## HTTP status code ##
1. **302** 302是一个普通的重定向代码。直观的看来是，请求者（浏览器或者模拟http请求）发起一个请求，然后服务端重定向到另一个地址。而事实上，服务端仅仅是增加一条属性到header，location=重定向地址。而一般的，浏览器会自动的再去请求这个location，重新获取资源。也就是说，这个会使得浏览器发起两次请求。
2. **303** 303 See Other。通常是指所请求的资源在别的地方，并且同302一样，会在header中的location标明资源的位置。在我的一个是使用过程中，我想要创建一个user，当关于这个user的key已经存在的时候，server将返回303，并且告之这个user的获取位置。

	`参考网址：[http://www.cnblogs.com/woshimrf/p/5851585.html](http://www.cnblogs.com/woshimrf/p/5851585.html "重定向Http status code 302 and 303")`
3. 