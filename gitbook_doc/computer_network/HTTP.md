<!-- TOC -->

   * [HTTP](#http)
        * [HTTP协议的特点](#http协议的特点)
        * [Cookie和Session的区别](#cookie和session的区别)
        * [没有Cookie是否依然能实现Session?](#没有cookie是否依然能实现session)
        * [重定向和转发的区别](#重定向和转发的区别)
        * [GET和POST区别](#get和post区别)
        * [常见HTTP状态码](#常见http状态码)
        * [301与302的区别](#301与302的区别)
        * [HTTP请求方法](#http请求方法)
        * [URI,URL,URN](#uriurlurn)

<!-- /TOC -->



# HTTP

#### HTTP协议的特点
* 适用于客户端与服务端的通信架构: 如果一个应用使用了HTTP协议，那么肯定要有一端作为客户端，
另一段作为服务端，请求由客户端发出，服务端处理并返回请求的结果。

* 无状态: **无状态是指HTTP协议不对请求和响应之间的通信状态进行保存，
对于发送过的请求或响应的结果都不做持久化处理。**
但无状态就意味着每个请求都是独立的，后续的请求如果需要用到前面使用过的信息/数据则需要重传，
这可能导致后续连接的数据较大。
于是Cookie和Session就应运而生,Cookie和Session可以保存用户的状态信息或数据。

* 无连接: 无连接是指每次TCP连接只处理一个请求，服务端处理完客户端的请求后，
立刻断开连接。采用这种方式，可以节省传输时间。
但是这样做的缺点也很明显，每个TCP连接只处理一个请求，
这样做不仅浪费资源，而且每次请求都需要建立连接，这就使得请求的效率也很低。

**从HTTP/1.1开始支持Keep-Alive功能，
Keep-Alive使得客户端与服务端的连接持续有效，
当客户端对服务端有多个请求时，都会使用这一条连接。 
当超过Keep-Alive规定的时间，或者出现其他意外的情况时，
客户端与服务端的连接才会被断开。**

#### Cookie和Session的区别
**Cookie是在客户端保存用户信息的一种机制，用于记录用户的一些状态信息。
每一次客户端向服务端发出请求，都会携带Cookie信息。**

**Session是在服务端保存用户信息的一种机制。
一个Session对应一个客户端，当客户端第一次请求服务端时，
客户端就会被分配一个唯一SessionId，该SessionId依赖于Cookie，被存储在客户端。**
因为SessionId采用Cookie保存，所以每次客户端请求服务端，
也都会携带该SessionId，这样，服务端就能根据SessionId识别客户端身份。

#### 没有Cookie是否依然能实现Session?
个人认为是可以的。

Session将SessionId保存在客户端的Cookie中，
而Cookie不过是客户端保存请求状态的一种机制而已，
使用其他技术当然也可以实现这种机制，
如LocalStorage/SessionStorage也可以存储。

#### 重定向和转发的区别

1. 转发是服务端行为,客户端是无法感知转发的。重定向则是客户端行为。
2. 转发属于一次请求，而重定向是客户端需要发送第二次请求。

#### GET和POST区别

GET和POST都是HTTP请求的一种方式，而HTTP协议是基于TCP协议的，
所以GET和POST都是基于TCP协议的。。-_-

GET请求的语义是从服务器获取资源，无论获取多少次资源，
数据可能不同，但是并不会对服务器资源造成任何影响。
**所以我认为GET请求是无副作用的，是幂等的，是可缓存的。**

POST请求的语义是在服务器上创建资源，是会产生副作用的。
**相同的2次POST请求会创建两份资源，因此POST请求是非幂等的，是不可缓存的。**

其他方面，个人认为没啥不同。
**只是对于不同的浏览器，GET请求和POST请求在这些浏览器上的表现也不同。**
如GET请求和POST请求的URL长度不同,但是具体的长度，恐怕还得视浏览器而定吧。

#### 常见HTTP状态码
HTTP状态码:
* 1** : 指示信息。服务端收到请求，继续执行操作。
* 2** : 成功。操作被成功接受并处理。
* 3** : 重定向。需要进一步的操作来完成请求。
* 4** : 客户端错误。由于客户端请求的错误，服务端无法处理请求。
* 5** : 服务端错误。服务端在处理请求的过程中发生了错误。

#### 301与302的区别
301和302都代表客户端请求的资源发生了转移。
不同之处在于:
301: 客户端请求的资源已被永久移动到了新的位置，客户端会自动重定向新URL。
客户端以后的请求应该都使用新的URL。
302: 客户端请求的资源被临时移动到了新的位置，客户端可以继续使用原URL。

#### HTTP请求方法
1. GET
2. POST
3. PUT
4. DELETE
5. HEAD
6. PATCH
7. OPTION
8. TRACE
9. CONNECT

#### URI,URL,URN

**URI ( uniform resource identifer):统一资源标识符**
>URI是一个互联网资源的唯一标识，但它并不代表资源在互联网上的位置，
>它对于资源的作用相当于身份证号码对于我们的作用，起一个唯一标识的作用。

**URL (uniform resource locator) : 统一资源定位符**
>URL是URI的子集，URL标识了资源在互联网上的位置，
>一个URL只能访问到一个资源，

**所以URL有着和URI相同的作用:都可以作为资源的唯一标识符，但URL也有URI没有的作用:对资源的定位。**

**URN(uniform resource name):统一资源名称**
>URN也是URI的子集，URN是对资源的命名，不能像URL一样对资源定位。