# Http长连接，也就是Keep-Alive
1. Http1.0里默认关闭，要加Connection: Keep-Alive.Http1.1里默认开启,要用Connection:close关闭
2. 优缺点

    在频繁通信的时候，这样可以减少链接请求与关闭的次数，节省了时间。
    在补频繁通信的时候，一直保持着链接浪费了网络资源。
3. 如何判断一次请求已完成

    Content-Length
    Content-Length适用于静态资源，根据这个Content-Length来判断是否接受完了。

    Transfer-Encoding
    Transfer-Encoding适用于动态资源，资源分包，发送完成后再发一个内容为0的包，则知道全部接受。

4. 请求完成后也不是马上关闭的，还有一个keep-alive timeout时间

    httpd守护进程会再多等一会，看服务器还有没有发送响应过来，如果一直没收到，时间到了timeout，这时候关闭http链接。

5. tcp的keep-alive，保活机制

    很久没联系时，先发一个试探包，看他回不回应，如果回应了说明还在线，继续保持连接，

    多尝试几次，如果一直没有就断开（客户端可能因各种意外而关闭，但是连接没有断开，这样就能断开了）。
