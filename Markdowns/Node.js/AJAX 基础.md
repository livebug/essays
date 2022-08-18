# AJAX 基础

*入门：https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX/Getting_Started*


 发送一个 http 请求
```JavaScript
// Old compatibility code, no longer needed.
if (window.XMLHttpRequest) { // Mozilla, Safari, IE7+ ...
    httpRequest = new XMLHttpRequest();
} else if (window.ActiveXObject) { // IE 6 and older
    httpRequest = new ActiveXObject("Microsoft.XMLHTTP");
}
```

你要发送一个实际的请求，通过调用 HTTP 请求对象的 open() 和 send() 方法，像下面这样：
```JavaScript
httpRequest.open('GET', 'http://www.example.org/some.file', true);
httpRequest.send();
```
>第三个参数是可选的，用于设置请求是否是异步的。如果设为 true (默认值)，即开启异步，JavaScript 就不会在此语句阻塞，使得用户能在服务器还没有响应的情况下与页面进行交互。

>send() 方法的参数可以是任何你想发送给服务器的内容，如果是 POST 请求的话。发送表单数据时应该用服务器可以解析的格式，像查询语句：

>如果你使用 POST 数据，那就需要设置请求的 MIME 类型。比如，在调用 send() 方法获取表单数据前要有下面这个：`httpRequest.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');`  这个语句需要在 open 与 send 函数之间

发送一个请求后，你会收到响应。在这一阶段，你要告诉 XMLHttp 请求对象是由哪一个 JavaScript 函数处理响应

```JavaScript
httpRequest.onreadystatechange = nameOfTheFunction;
```

这个函数应该做什么？  
首先，函数要检查请求的状态。`httpRequest.readyState === XMLHttpRequest.DONE`

`XMLHttpRequest.readyState` 代码值:

| 值  | 状态             | 描述                                              |
| --- | ---------------- | ------------------------------------------------- |
| 0   | UNSENT           | 代理被创建，但尚未调用 open() 方法。              |
| 1   | OPENED           | open() 方法已经被调用。                           |
| 2   | HEADERS_RECEIVED | send() 方法已经被调用，并且头部和状态已经可获得。 |
| 3   | LOADING          | 下载中；responseText 属性已经包含部分数据。       |
| 4   | DONE             | 下载操作已完成。                                  |


接下来，点击 HTTP 响应的 response code。 可能的响应码都已经列在 W3C(https://www.rfc-editor.org/rfc/rfc9110.html#name-status-codes)这个列表里。在下面的例子中，我们通过检查响应码 200 OK 判断 AJAX 有没有成功。

```JavaScript
if (httpRequest.status === 200) {
    // Perfect!
} else {
    // There was a problem with the request.
    // For example, the response may have a 404 (Not Found)
    // or 500 (Internal Server Error) response code.
}
```
>HTTP响应码：
>+ 1xx (Informational) 1xx (信息): The request was received, continuing process : 请求已收到，继续处理
>+ 2xx (Successful) 2xx (成功): The request was successfully received, understood, and accepted : 请求被成功接收、理解和接受
>+ 3xx (Redirection) 3xx (重定向): Further action needs to be taken in order to complete the request : 需要采取进一步行动以完成请求
>+ 4xx (Client Error) 4xx (客户端错误): The request contains bad syntax or cannot be fulfilled : 请求包含错误语法或无法完成
>+ 5xx (Server Error) 5xx (服务器错误): The server failed to fulfill an apparently valid request : 服务器未能满足一个明显有效的请求
  


在检查完请求状态和 HTTP 响应码后， 你就可以用服务器返回的数据做任何你想做的了。你有两个方法去访问这些数据：

+ httpRequest.responseText – 服务器以文本字符的形式返回
+ httpRequest.responseXML – 以 XMLDocument 对象方式返回，之后就可以使用 JavaScript 来处理


基础课下课！