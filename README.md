# 笔记
> 记录日常的一些小的知识点和疑惑点
## *为什么在 chrome 的调试器的 NetWork 中调试接口调用，经常会看到同一个接口会调用两次？*
- 因为当前的请求的接口是跨域的，根据同源策略应该是不能调通的。但是，后端可以设置 `Access-Control-Allow-Origin: *` 就可以跨域请求后端接口了。在一些情况下，会先发送一个 `OPTION` 请求以确认接口是否可以调用，如果第一个接口通过了，就可以正常调用接口了。这里的第一个请求叫**预请求(preflight request)**。
- 下面几种情况下会有预请求：
    - 请求方法不是 `GET/HEAD/POST`
    - `POST` 请求的 `Content-Type` 并非 `application/x-www-form-urlencoded`, `multipart/form-data`, 或者 `text/plain`
    - 请求设置了自定义 `header` 字段
> 参考连接：
    - https://blog.csdn.net/cc1314_/article/details/78272329
