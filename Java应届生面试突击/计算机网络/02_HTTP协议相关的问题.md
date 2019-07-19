# HTTP 协议相关的问题

### 目录

---
<a href="#1">1. Http 的请求报文结构和响应报文结构。</a> <br>
<a href="#2">2. 常见 HTTP 首部字段。</a> <br>
<a href="#3">3. Http 状态码含义。</a> <br>
<a href="#4">4. http 中有关缓存的首部字段有哪些?http 的浏览器缓存机制。</a> <br>
<a href="#5">5. Http1.1 和 Http1.0 的区别。(HTTP1.1 版本的 4 个新特性)</a> <br>
<a href="#6">6. 常用的 HTTP 方法有哪些?</a> <br>
<a href="#7">7. http 的请求方式 get 和 post 的区别。</a> <br>
<a href="#8">8. 为什么 HTTP 是无状态的?如何保持状态(会话跟踪技术、状态管理)?</a> <br>
<a href="#9">9. Http 的短连接和长连接的原理。</a> <br>
<a href="#10">10. HTTP 的特点。</a> <br>
<a href="#11">11. http 的安全问题。</a> <br>
<a href="#12">12. Https 的作用。</a> <br>
<a href="#13">13. 浏览器和服务器在基于 https 进行请求链接到数据传输过程中,用到了哪些技术?</a> <br>
<a href="#14">14. 讲下 Http 协议。</a> <br>
<a href="#15">15. http 和 socket 的区别,两个协议哪个更高效一点。</a> <br>
<a href="#16">16. HTTP 与 HTTPS 的区别。</a> <br>

### <a name="1">1. 优化查询的方法？</a>

#### *HTTP 请求报文* 主要由请求行、请求头、空行、请求正文(*Get 请求没有请求正文*)4 部分组成。 <br>
[02_1_1](/data/images/Java应届生面试突击/计算机网络/02_1_1.png) <br>
1. 请求行 <br>
&ensp;&ensp;&ensp;&ensp;
    由 3 部分组成,分别为:请求方法、URL 以及协议版本,之间由空格分隔;
请求方法包括 GET、HEAD、PUT、POST、TRACE、OPTIONS、DELETE 以及扩展
方法,当然并不是所有的服务器都实现了所有的方法,部分方法即便支持,出
于安全性的考虑也是不可用的; <br>
&ensp;&ensp;&ensp;&ensp;
    协议 版本的格 式为:HTTP/主版本号.次版本号 ,常用的有 HTTP/1.0 和
HTTP/1.1; <br>
2. 请求头 <br>
&ensp;&ensp;&ensp;&ensp;
    请求头部为请求报文添加了一些附加信息,由“名/值”对组成,每行一对,
名和值之间使用冒号分隔。 <br>
&ensp;&ensp;&ensp;&ensp;
    常见请求头如下: <br>
[02_1_2](/data/images/Java应届生面试突击/计算机网络/02_1_2.png) <br>
3. 空行 <br>
&ensp;&ensp;&ensp;&ensp;
    请求头的最后会有一个空行,表示请求头部结束,接下来为请求正文,这
一行非常重要,必不可少。 <br>
4. 请求正文 <br>
&ensp;&ensp;&ensp;&ensp;
    可选部分,比如 GET 请求就没有请求正文。 <br>
[02_1_3](/data/images/Java应届生面试突击/计算机网络/02_1_3.png) <br>

#### *HTTP 响应报文* 主要由状态行、响应头、空行、响应正文 4 部分组成。
[02_1_4](/data/images/Java应届生面试突击/计算机网络/02_1_4.png) <br>

1. 状态行 <br>
&ensp;&ensp;&ensp;&ensp;
    由 3 部分组成,分别为:协议版本,状态码,状态码描述,之间由空格分隔; <br>
2. 响应头 <br>
&ensp;&ensp;&ensp;&ensp;
    与请求头类似,为响应报文添加了一些附加信息。 <br>
&ensp;&ensp;&ensp;&ensp;
    常见响应头如下: <br>
[02_1_5](/data/images/Java应届生面试突击/计算机网络/02_1_5.png) <br>
3. 空行 <br>
4. 响应正文 <br>
[02_1_6](/data/images/Java应届生面试突击/计算机网络/02_1_6.png) <br>


### <a name="2">2. 常见 HTTP 首部字段。</a>
1. *通用首部字段*(请求报文与响应报文都会使用的首部字段) <br>
Date:创建报文时间 <br>
Connection:连接的管理 <br>
Cache-Control:缓存的控制 <br>
Transfer-Encoding:报文主体的传输编码方式,如 *Transfer-Encoding:chunked*。 <br>

2. *请求首部字段*(请求报文会使用的首部字段) <br>
Host:请求资源所在服务器 <br>
Accept:可处理的媒体类型 <br>
Accept-Charset:可接收的字符集 <br>
Accept-Encoding:可接受的内容编码 <br>
Accept-Language:可接受的自然语言 <br>
*Referer*:HTTP Referer 是 header 的一部分,当浏览器向 web 服务器发送请求的时候,
一般会带上 Referer,*告诉服务器我是从哪个页面链接过来的*,服务器籍此可以获得一些信
息用于处理。比如从我主页上链接到一个朋友那里,他的服务器就能够从 HTTP Referer
中统计出每天有多少用户点击我主页上的链接访问他的网站。如果是 CSRF 攻击传来的请
求,Referer 字段会是*包含恶意网址的地址*,这时候服务器就能识别出恶意的访问。 <br>

3. *响应首部字段*(响应报文会使用的首部字段) <br>
Accept-Ranges:可接受的字节范围 <br>
Location:令客户端重新定向到的 URI <br>
Server:HTTP 服务器的安装信息 <br>

4. *实体首部字段*(请求报文与响应报文的的*实体部分使用的首部字段*) <br>
Allow:资源可支持的 HTTP 方法 <br>
Content-Type:实体主类的类型 <br>
Content-Encoding:实体主体适用的编码方式 <br>
Content-Language:实体主体的自然语言 <br>
Content-Length:实体主体的字节数 <br>
Content-Range:实体主体的位置范围,一般用于发出部分请求时使用。 <br>

### <a name="3>3. Http 状态码含义。</a> 

200 OK 服务器已成功处理了请求并提供了请求的网页。 <br>
202 Accepted 已经接受请求,但处理尚未完成。 <br>
204 No Content 没有新文档,浏览器应该继续显示原来的文档。 <br>
206 Partial Content 客户端进行了范围请求。响应报文中由 Content-Range 指定实体
内容的范围。实现断点续传。 <br>
-------------------------------------------------------------------------------------------------
301 Moved Permanently 永久性重定向。请求的网页已永久移动到新位置。 <br>
302 (或 307) Moved Temporatily 临时性重定向。请求的网页临时移动到新位置。 <br>
304 Not Modified 未修改。自从上次请求后,请求的内容未修改过。 <br>
-------------------------------------------------------------------------------------------------
401 Unauthorized
客户试图未经授权访问受密码保护的页面。应答中会包含一个
WWW-Authenticate 头, 浏览器据此显示用户名字/密码对话框, 然后在填写合适的
Authorization 头后再次发出请求。 <br>
403 Forbidden 服务器拒绝请求。 <br>
403.6-IP address rejected。 <br>
404 Not Found 服务器上不存在客户机所请求的资源。 <br>
-------------------------------------------------------------------------------------------------
500 Internal Server Error 服务器遇到一个错误,使其无法为请求提供服务。 <br>

### <a name="4>4. http 中有关缓存的首部字段有哪些?http 的浏览器缓存机制。</a>
[02_4_1](/data/images/Java应届生面试突击/计算机网络/02_4_1.png) <br>

#### 1.Last-Modified 和 If-Modified-Since
&ensp;&ensp;&ensp;&ensp;
    简单的说,Last-Modified 与 If-Modified-Since 都是用于记录页面最后修改时间的
HTTP 头 信 息 , 只 是 Last-Modified 是 由 服 务 器 往 客 户 端 发 送 的 HTTP 头 , 而
If-Modified-Since 则是由客户端往服务器发送的头,可以看到,再次请求本地存在的缓存
页面时,客户端会通过 If-Modified-Since 头把浏览器端缓存页面的最后一次被服务器修改
的时间一起发到服务器去,服务器会把这个时间与服务器上实际文件的最后修改时间进行
比较,通过这个时间戳判断客户端的页面是否是最新的,如果不是最新的,就返回 HTTP
状态码 200 和新的文件内容,客户端接到之后,会丢弃旧文件,把新文件缓存起来,并显
示到浏览器中;如果是最新的,则返回 304 告诉客户端其本地缓存的页面是最新的,就直
接把本地缓存文件显示到浏览器中,这样在网络上传输的数据量就会大大减少,同时也减
轻了服务器的负担。
1) 什么是”Last-Modified”?
&ensp;&ensp;&ensp;&ensp;
    在浏览器第一次请求某一个 URL 时,服务器端的返回状态会是 200,内容是你请求的
资源,同时有一个 Last-Modified 的属性标记此文件在服务期端最后被修改的时间,格式类
似这样:
&ensp;&ensp;&ensp;&ensp;
    Last-Modified: Fri, 12 May 2006 18:53:33 GMT
&ensp;&ensp;&ensp;&ensp;
    客户端第二次请求此 URL 时,浏览器会向服务器传送 If-Modified-Since 报头,询问
该时间之后文件是否有被修改过:
&ensp;&ensp;&ensp;&ensp;
    If-Modified-Since: Fri, 12 May 2006 18:53:33 GMT
&ensp;&ensp;&ensp;&ensp;
    如果服务器端的资源没有变化,则自动返回 HTTP 304 状态码,内容为空,这样就
节省了传输数据量。当服务器端代码发生改变或者重启服务器时,则重新发出资源,返回
和第一次请求时类似,从而保证不向客户端重复发出资源,也保证当服务器有变化时,客
户端能够得到最新的资源。

#### 2. ETag 和 If-None-Match
&ensp;&ensp;&ensp;&ensp;
    ETag 和 If-None-Match 是一种常用的判断资源是否改变的方法。类似于 Last-Modified
和 If-Modified-Since。但是有所不同的是 Last-Modified 和 If-Modified-Since 只判断资源的
最后修改时间,而 ETag 和 If-None-Match 可以是资源任何的任何属性,比如资源的 MD5
等。
&ensp;&ensp;&ensp;&ensp;
    ETag 和 If-None-Match 的工作原理是在 HTTP Response 中添加 ETags 信息。当客户
端再次请求该资源时,将在 HTTP Request 中加入 If-None-Match 信息(也就是 ETags 的
值)。如果服务器验证资源的 ETags 没有改变(该资源的内容没有改变),将返回一个 304
状态;否则,服务器将返回 200 状态,并返回该资源和新的 ETags。
2) 什么是”Etag”?
&ensp;&ensp;&ensp;&ensp;
    服务器会为每个资源分配对应的 ETag 值,根据资源的内容得到其值。当资源内容发
生改变时,其值也会改变。以下是服务器端返回的格式:
&ensp;&ensp;&ensp;&ensp;
    ETag: "50b1c1d4f775c61:df3"
&ensp;&ensp;&ensp;&ensp;
    客户端的查询更新格式是这样的:
&ensp;&ensp;&ensp;&ensp;
    If-None-Match: W/"50b1c1d4f775c61:df3"
&ensp;&ensp;&ensp;&ensp;
    如果 ETag 没改变,则返回状态 304,这也和 Last-Modified 一样。

##### 扩展 1:Last-Modified 和 Etags 如何帮助提高性能?
&ensp;&ensp;&ensp;&ensp;
    聪明的开发者会把 Last-Modified 和 ETags 请求的 http 报头一起使用,这样可利用
客户端(例如浏览器)的缓存。因为服务器首先产生 Last-Modified/Etag 标记,服务器可
在稍后使用它来判断页面是否已经被修改。本质上,客户端通过将该记号传回服务器要求
服务器验证其(客户端)缓存。

##### 扩展 2:既然有了 Last-Modified,为什么还要用 ETag 字段呢?
1. 某些文件修改非常频繁,比如在秒以下的时间内进行修改(比方说 1s 内修改了 N
次),If-Modified-Since 能检查到的粒度是秒级的,这种修改无法体现。
2. 一些文件也许会周期性的更改,但是他的内容并不改变(仅仅改变的修改时间),这
个时候我们并不希望客户端认为这个文件被修改了,而重新 GET;
3. 某些服务器不能精确的得到文件的最后修改时间。
&ensp;&ensp;&ensp;&ensp;
   因此, HTTP/1.1 利用 Entity Tag 头提供了更加严格的验证。 Last-Modified 与 ETag
一起使用时,服务器会 优先验证 ETag 的值 。

#### 3.Expires / Cache-Control(优先使用)
&ensp;&ensp;&ensp;&ensp;
    用来控制缓存的失效日期,控制浏览器是直接从浏览器缓存取数据还是重新发请求到
服务器取数据。 <br>
&ensp;&ensp;&ensp;&ensp;
    Expires 是 Web 服务器响应消息头字段,在响应 http 请求时告诉浏览器在过期时间前
浏览器可以直接从浏览器缓存取数据,而无需再次请求。Expires 的一个缺点就是,返回
的到期时间是服务器端的时间,这样存在一个问题,如果客户端的时间与服务器的时间相
差很大(比如时钟不同步,或者跨时区),那么误差就很大,所以在 HTTP 1.1 版开始,使
用 Cache-Control: max-age=(秒)替代。 <br>

当服务器发出响应的时候,可以通过两种方式来告诉客户端缓存请求: <br>
第一种是 Expires,比如: <br>
&ensp;&ensp;&ensp;&ensp;
    Expires: Sun, 16 Oct 2016 05:43:02 GMT <br>
&ensp;&ensp;&ensp;&ensp;
    在此日期之前,客户端都会认为缓存是有效的。 <br>
&ensp;&ensp;&ensp;&ensp;
    不过 Expires 有缺点,比如说,服务端和客户端的时间设置可能不同,这就会使缓存
的失效可能并不能精确的按服务器的预期进行。 <br>
第二种是 Cache-Control,比如: <br>
&ensp;&ensp;&ensp;&ensp;
    Cache-Control: max-age=315360000 <br>
&ensp;&ensp;&ensp;&ensp;
    这里声明的是一个相对的秒数,表示从现在起,315360000 秒内缓存都是有效的,这
样就避免了服务端和客户端时间不一致的问题。 <br>
&ensp;&ensp;&ensp;&ensp;
    但是 Cache-Control 是 HTTP1.1 才有的,不适用于 HTTP1.0,而 Expires 既适用于
HTTP1.0,也适用于 HTTP1.1,所以说在大多数情况下同时发送这两个头会是一个更好的
选择,当客户端两种头都能解析的时候,会优先使用 Cache-Control。 <br>

过程如下: <br>
- 1. 客户端请求一个页面(A)。
  2. 服务器返回页面 A,并在给 A 加上一个 Last-Modified 和 ETag。
  3. 客户端展现该页面,并将页面连同 Last-Modified 和 ETag 的值一起缓存。
  4. 客户再次请求页面 A,并将上次请求时服务器返回的 Last-Modified 和 ETag 的值
一起传递给服务器。
  5. 服务器检查该 Last-Modified 或 ETag,并判断出该页面自上次客户端请求之后还
未被修改,直接返回响应 304 和一个空的响应体。

1. 首先在服务器创建一个简单的 HTML 文件,用浏览器访问一下,成功表示 HTML 页
面。Fiddler 就会产生下面的捕获信息。 <br>
需要留意的是 <br>
- 1. 因为是第一次访问该页面,客户端发请求时,请求头中没有 If-Modified-Since 标
签。
- 2. 服务器返回的 HTTP 状态码是 200,并发送页面的全部内容。
- 3.服务器返回的 HTTP 头标签中有 Last-Modified,告诉客户端页面的最后修改时间。
[02_4_2](/data/images/Java应届生面试突击/计算机网络/02_4_2.png) <br>


2.在浏览器中刷新一下页面,Fiddler 就会产生下面的捕获信息。 <br>
需要注意的是 <br>
- 1. 客户端发 HTTP 请求时,使用 If-Modified-Since 标签,把上次服务器告诉它的文
件最后修改时间返回到服务器端了。
  2. 因为文件没有改动过,所以服务器返回的 HTTP 状态码是 304,没有发送页面的内
容。
[02_4_3](/data/images/Java应届生面试突击/计算机网络/02_4_3.png) <br>
3. 用文本编辑器稍微改动一下页面文件,保存。再用浏览器访问一下,Fiddler 就会产
生下面的捕获信息。 <br>
需要留意的是 <br>
- 1. 客户端发 HTTP 请求时,使用 If-Modified-Since 标签,把上次服务器告诉它的文
件最后修改时间返回到服务器端了。
  2. 因为文件被改动过,两边时间不一致,所以服务器返回的 HTTP 状态码是 200,并
发送新页面的全部内容。
  3. 服务器返回的 HTTP 头标签中有 Last-Modified,告诉客户端页面的新的最后修改
时间。
[02_4_4](/data/images/Java应届生面试突击/计算机网络/02_4_4.png) <br>

### <a name="5>5. Http1.1 和 Http1.0 的区别。(HTTP1.1 版本的 4 个新特性)</a>
1. 默认持久连接和流水线 <br>
&ensp;&ensp;&ensp;&ensp;
    HTTP/1.1 默认使用持久连接,只要客户端服务端任意一端没有明确提出断开 TCP 连
接,就一直保持连接,在同一个 TCP 连接下,可以发送多次 HTTP 请求。同时,默认采用
流水线的方式发送请求,即客户端每遇到一个对象引用就立即发出一个请求,而不必等到
收到前一个响应之后才能发出下一个请求,但服务器端必须按照接收到客户端请求的先后
顺序依次回送响应结果,以保证客户端能够区分出每次请求的响应内容,这样也显著地减
少了整个下载过程所需要的时间。 <br>
&ensp;&ensp;&ensp;&ensp;
   HTTP/1.0 默认使用短连接,要建立长连接,可以在请求消息中包含 Connection:
Keep-Alive 头域,如果服务器愿意维持这条连接,在响应消息中也会包含一个 Connection:
Keep-Alive 的头域。 Connection 请求头的值为 Keep-Alive 时,客户端通知服务器返回本次
请求结果后保持连接;Connection 请求头的值为 close 时,客户端通知服务器返回本次请
求结果后关闭连接。 <br>

2. 分块传输数据 <br>
&ensp;&ensp;&ensp;&ensp;
   HTTP/1.0 可用来指定实体长度的唯一机制是通过 Content-Length 字段。静态资源的
长度可以很容易地确定,但是对于动态生成的响应来说,为获取它的真实长度,只能等它
完全生成之后,才能正确地填写 Content-Length 的值,这便要求缓存整个响应,在服务
器端占用大量的缓存,从而延长了响应用户的时间。 <br>
&ensp;&ensp;&ensp;&ensp;
   HTTP/1.1 引入了被称为分块(chunked)的传输方法。该方法使发送方能将消息实体
分割为任意大小的组块(chunk),并单独地发送他们。在每个组块前面,都加上了该组块
的长度,使接收方可确保自己能够完整地接收到这个组块。更重要的是,在最末尾的地方,
发送方生成了长度为零的组块,接收方可据此判断整条消息都已安全地传输完毕。这样也
避免了在服务器端占用大量的缓存。Transfer-Encoding:chunked 向接收方指出:响应
将被分组块,对响应分析时,应采取不同于非分组块的方式。 <br>
3. 状态码 100 Continue <br>
&ensp;&ensp;&ensp;&ensp;
   HTTP/1.1 加入了一个新的状态码 100 Continue,用于客户端在发送 POST 数据给服
务器前,征询服务器的情况,看服务器是否处理 POST 的数据。 <br>
&ensp;&ensp;&ensp;&ensp;
   当要 POST 的数据大于 1024 字节的时候,客户端并不会直接就发起 POST 请求, 而
是会分为 2 步:
&ensp;&ensp;&ensp;&ensp;
   1. 发送一个请求, 包含一个 Expect:100-continue, 询问 Server 是否愿意接受数据。 <br>
&ensp;&ensp;&ensp;&ensp;
   2. 接收到 Server 返回的 100 continue 应答以后, 才把数据 POST 给 Server。
这种情况通常发生在客户端准备发送一个冗长的请求给服务器,但是不确认服务器是
否有能力接收。如果没有得到确认,而将一个冗长的请求包发送给服务器,然后包被服务
器给抛弃了,这种情况挺浪费资源的。 <br>
4. Host 域 <br>
HTTP1.1 在 Request 消息头里多了一个 Host 域,HTTP1.0 则没有这个域。 <br>
&ensp;&ensp;&ensp;&ensp;
    在 HTTP1.0中认为每台服务器都绑定一个唯一的 IP 地址,这个 IP 地址上只有一个主机。但随着虚拟
主机技术的发展,在一台物理服务器上可以存在多个虚拟主机,并且它们共享一个 IP 地址。

### <a name="6>6. 常用的 HTTP 方法有哪些?</a>
[02_6_1](/data/images/Java应届生面试突击/计算机网络/02_6_1.png) <br>
*注意:只有 POST 和 PUT 方法才有请求内容。*
GET: 用于请求访问已经被 URI(统一资源标识符)识别的资源,可以通过 URL 传参
给服务器。
POST:用于传输信息给服务器,主要功能与 GET 方法类似,但一般推荐使用 POST
方式。
PUT: 传输文件,报文主体中包含文件内容,保存到对应 URI 位置。
HEAD: 获得报文首部,与 GET 方法类似,只是不返回报文主体。
DELETE:删除文件,与 PUT 方法相反,删除对应 URI 位置的文件。
OPTIONS:查询相应 URL 支持的 HTTP 方法。

*注意:并非所有的服务器都都实现了这几个方法。有的服务器还实现了自己特有的
HTTP 方法,称为扩展方法。*
- *GET*:GET 可以说是最常见的了,它本质就是发送一个请求来取得服务器上的某一资
源。资源通过一组 HTTP 头和呈现数据(如 HTML 文本,或者图片或者视频等)返回
给客户端。GET 请求中,永远不会包含呈现数据。
- *HEAD*:HEAD 和 GET 本质是一样的,区别在于 HEAD 不含有呈现数据,而仅仅是
HTTP 头信息。有的人可能觉得这个方法没什么用,其实不是这样的。想象一个业务情
景:欲判断某个资源是否存在,我们通常使用 GET,但这里用 HEAD 则意义更加明确。
- *PUT*:这个方法比较少见。HTML 表单也不支持这个。本质上来讲, PUT 和 POST 极
为相似,都是向服务器发送数据,但它们之间有一个重要区别,PUT 通常指定了资源
的存放位置,而 POST 则没有,POST 的数据存放位置由服务器自己决定。举个例子:
如一个用于提交博文的 URL,/addBlog。如果用 PUT,则提交的 URL 会是像这样
的”/addBlog/abc123”,其中 abc123 就是这个博文的地址。而如果用 POST,则这
个地址会在提交后由服务器告知客户端。目前大部分博客都是这样的。显然,PUT 和 
POST 用途是不一样的。具体用哪个还取决于当前的业务场景。
DELETE:删除某一个资源。基本上这个也很少见,不过还是有一些地方比如 amazon
的 S3 云服务里面就用的这个方法来删除资源。
- *POST*:向服务器提交数据。这个方法用途广泛,几乎目前所有的提交操作都是靠这个
完成。
- *OPTIONS*:这个方法很有趣,但极少使用。它用于获取当前 URL 所支持的方法。若
请求成功,则它会在 HTTP 头中包含一个名为“Allow”的头,值是所支持的方法, 如“GET, POST”。
- *TRACE*:请求服务器回送收到的请求信息,主要用于测试和诊断,所以是安全的。

HEAD、GET、OPTIONS 和 TRACE 视为安全的方法,因为它们只是从服务器获得资
源而不对服务器做任何修改;但是 HEAD、 GET、 OPTIONS 在用户端不安全,而 POST
则影响服务器上的资源。

GET 虽然不修改服务器数据,但是 GET 方法通过 URL 请求来传递用户的输入; HEAD
只获得消息的头部,但是数据传入也是通过 URL。这样对客户端而言并不安全。

*TRACE 方法对于服务端和用户端一定是安全的。*


### <a name="7>7. http 的请求方式 get 和 post 的区别。</a>
1. GET 一般用于获取或者查询资源信息,这就意味着它是幂等的(对同一个 URL 的
多个请求返回同样的结果)和安全的(没有修改资源的状态),而 POST 一般用于更新资
源信息,POST 既不是安全的,也不是幂等的。
2. 采用 GET 方法时,客户端把要发送的数据添加到 URL 后面(就是把数据放置在
HTTP 协议头中, GET 是通过 URL 提交数据的),并且用“?”连接,各个变量之间用“&”
连接; <br>
&ensp;&ensp;&ensp;&ensp;
    HTTP 协议没有对 URL 长度进行限制,由于特定的浏览器及服务器对 URL 的长度存
在限制,所以传递的数据量有限; <br>
 &ensp;&ensp;&ensp;&ensp;
   通过 GET 提交数据,用户名和密码将明文出现在 URL 上,因为(1)登录页面有可能被
浏览器缓存,(2)其他人查看浏览器的“历史纪录”,那么别人就可以拿到你的账号和密码
了。 <br>
&ensp;&ensp;&ensp;&ensp;
    而 POST 把要传递的数据放到 HTTP 请求报文的消息体中; HTTP 协议也没有进行大
小限制,起限制作用的是服务器的处理程序的能力,但是,传送的数据量比 GET 方法更大
些;由于传递的数据在消息体中,安全性高,但其实用抓包软件(如 httpwatch)进行抓包
的话,可以看到传递的数据内容的。
3. GET 请求的数据会被浏览器缓存起来,会留下历史记录;而 POST 提交的数据不
会被浏览器缓存,不会留下历史记录。

GET 请求如下: <br>
[02_7_1](/data/images/Java应届生面试突击/计算机网络/02_7_1.png) <br>

POST 请求如下: <br>
[02_7_2](/data/images/Java应届生面试突击/计算机网络/02_7_2.png) <br>

### <a name="8>8. 为什么 HTTP 是无状态的?如何保持状态(会话跟踪技术、状态管理)?</a>
&ensp;&ensp;&ensp;&ensp;
    HTTP 无状态:无状态是指协议对于*事务处理*没有记忆能力,不能保存每次客户端提
交的信息,即当服务器返回应答之后,这次*事务*的所有信息就都丢掉了。如果用户发来一
个新的请求,服务器也无法知道它是否与上次的请求有联系。 <br>
&ensp;&ensp;&ensp;&ensp;
    这里我们用一个比较熟悉的例子来理解 HTTP 的无状态性,如一个包含多图片的网页
的浏览。步骤为:1建立连接,客户端发送一个网页请求,服务器端返回一个 html 页面(这
里的页面只是一个纯文本的页面,也就是我们写的 html 代码),关闭连接;2浏览器解析
html 文件,遇到图片标记得到 url,这时,客户端和服务器再建立连接,客户端发送一个图
片请求,服务器返回图片应答,关闭连接。(这里又涉及到无状态定义:对于服务器来说,
这次的请求虽然是同一个客户端的请求但是服务器还是不知道这个是之前的那个客户端,
即对于事务处理没有记忆能力)。 <br>
&ensp;&ensp;&ensp;&ensp;
    优点:服务器不用为每个客户端连接*分配内存来记忆大量状态*,也不用在客户端失去连
接时去清理内存,节省服务器端资源,以更高效地去处理业务。 <br>
&ensp;&ensp;&ensp;&ensp;
    缺点:缺少状态意味着*如果后续处理需要前面的信息,则客户端必须重传*,这样可能导
致每次连接*传送的数据量增大*。 <br>
&ensp;&ensp;&ensp;&ensp;
    针对这些缺点,可以采用*会话跟踪技术*来解决这个问题。把状态保存在服务器中,只发
送回一个标识符,浏览器在下次提交中把这个标识符发送过来;这样,就可以定位存储在
服务器上的状态信息了。 <br>
*有四种会话跟踪技术:* <br>
1.COOKIE <br>
2.Session <br>
3.URL 重写 <br>
4.作为隐藏域嵌入 HTML 表单中(隐藏表单域) <br>
&ensp;&ensp;&ensp;&ensp;
    在浏览器和服务器之间来回传递一个标识符,这就是所谓的会话(session)跟踪。来
自浏览器的所有包含同一个标识符(这里是 SESSIONID)的请求同属于一个会话。 <br>
&ensp;&ensp;&ensp;&ensp;
    会话的有效期直到它被显式地终止为止,或者当用户在一段时间内没有动作,由服务
器自动设置为过期。目前没有办法通知服务器用户已经关闭浏览器,因为在浏览器和服务
器之间没有一个持久的连接,并且浏览器关闭时也不向服务器发送信息。同时,关闭浏览
器通常意味着会话 ID 丢失,COOKIE 将过期,或者注入了信息的 URL 将不能再使用。所以
当用户再次打开浏览器的时候,服务器无法将新得到的请求与以前的会话联系起来,则只
能创建一个新的会话。然而,所有与前一个会话有关的数据依然存放在服务器上,直到会
话过期被清除为止。 <br>

### <a name="9>9. Http 的短连接和长连接的原理。</a>
&ensp;&ensp;&ensp;&ensp;
    HTTP 协议既可以实现长连接,也可以实现短连接。
&ensp;&ensp;&ensp;&ensp;
    在 HTTP/1.0 中,默认使用的是短连接。也就是说,浏览器和服务器每进行一次 HTTP
操作,就建立一次连接,但任务结束就中断连接。如果客户端访问的某个 HTML 或其他类
型的 Web 页中包含有其他的 Web 资源,如 JavaScript 文件、图像文件、CSS 文件等,
当浏览器每遇到这样一个 Web 资源,就会建立一个 HTTP 会话。 HTTP1.0 需要在 request
中增加 ”Connection:keep-alive“ header 才能够支持长连接。
&ensp;&ensp;&ensp;&ensp;
    HTTP1.0 KeepAlive 支持的数据交互流程如下:
&ensp;&ensp;&ensp;&ensp;
    a) Client 发出 request,其中该 request 的 HTTP 版本号为 1.0。同时在 request
中包含一个 header:”Connection: keep-alive“。
&ensp;&ensp;&ensp;&ensp;
    b) Web Server 收到 request 中的 HTTP 协议为 1.0 及”Connection:
keep-alive“就认为是一个长连接请求,其将在 response 的 header 中也增
加”Connection: keep-alive“。同时不会关闭已建立的 tcp 连接。
&ensp;&ensp;&ensp;&ensp;
    c) Client 收到 Web Server 的 response 中包含”Connection: keep-alive“,就
认为是一个长连接,不关闭 tcp 连接。并用该 tcp 连接再发送 request。(跳转到 a))。
&ensp;&ensp;&ensp;&ensp;
    但从 HTTP/1.1 起,默认使用长连接,用以保持连接特性。使用长连接的 HTTP 协议,
会在请求头和响应头加入这行代码:
&ensp;&ensp;&ensp;&ensp;
    Connection:keep-alive
&ensp;&ensp;&ensp;&ensp;
    在使用长连接的情况下,当一个网页打开完成后,客户端和服务器之间用于传输 HTTP
数据的 TCP 连接不会关闭,如果客户端再次访问这个服务器上的网页,会继续使用这一条
已经建立的连接(http 长连接利用同一个 tcp 连接处理多个 http 请求和响应)。
Keep-Alive 不会永久保持连接,它有一个保持时间,可以在不同的服务器软件(如
Apache)中设定这个时间。实现长连接要客户端和服务端都支持长连接。长连接中关闭
连接通过 Connection:closed 头部字段。如果请求或响应中的 Connection 被指定为
closed,表示在当前请求或响应完成后将关闭 TCP 连接。 TCP 的 keep alive 是检查
当前 TCP 连接是否活着;HTTP 的 Keep-alive 是要让一个 TCP 连接活久点。 <br>

HTTP1.1 KeepAlive 支持的数据交互流程如下: <br>
a) Client 发出 request,其中该 request 的 HTTP 版本号为 1.1。 <br>
b) Web Server 收到 request 中的 HTTP 协议为 1.1 就认为是一个长连接请求,其将
在 response 的 header 中也增加”Connection: keep-alive“。同时不会关闭已建立的
tcp 连接。 <br>
c) Client 收到 Web Server 的 response 中包含”Connection: keep-alive“,就认
为是一个长连接,不关闭 tcp 连接,并用该 tcp 连接再发送 request。(跳转到 a))。
HTTP 协议的长连接和短连接,实质上是 TCP 协议的长连接和短连接。 <br>

http 长连接的优点: <br>
1.通过开启和关闭更少的 TCP 连接,节约 CPU 时间和内存。 <br>
2.通过减少 TCP 开启和关闭引起的包的数目,降低网络阻塞。 <br>

http 长连接的缺点: <br>
服务器维护一个长连接会增加开销。 <br>

http 短连接的优点: <br>
服务器不用为每个客户端连接分配内存来记忆大量状态,也不用在客户端失去连接时去清
理内存,节省服务器端资源,以更高效地去处理业务。 <br>

http 短连接的缺点: <br>
如果客户请求频繁,将在 TCP 的建立和关闭操作上浪费时间和带宽。 <br>

### <a name="10>10. HTTP 的特点。</a>
&ensp;&ensp;&ensp;&ensp;
    (1)支持客户端/服务器端通信模式。 <br>
&ensp;&ensp;&ensp;&ensp;
    (2)简单方便快速:当客户端向服务器端发送请求时,只是简单的填写请求路径和请求
方法即可,然后就可以通过浏览器或其他方式将该请求发送就行了。比较常用的请求方法
有三种,分别是:GET、HEAD、POST。不同的请求方法使得客户端和服务器端联系的方式
各不相同。因为 HTTP 协议比较简单,所以 HTTP 服务器的程序规模相对比较小,从而使得
通信的速度非常快。 <br>
&ensp;&ensp;&ensp;&ensp;
    (3)灵活:Http 协议允许客户端和服务器端传输任意类型任意格式的数据对象。这些不
同的类型由 Content-Type 标记。 <br>
&ensp;&ensp;&ensp;&ensp;
    (4)无连接:无连接的含义是每次建立的连接只处理一个客户端请求。当服务器处理完
客户端的请求之后,并且收到客户的反馈应答后,服务器端立即断开连接。采用这种通信
方式可以大大的节省传输时间。 <br>
&ensp;&ensp;&ensp;&ensp;
    (5)无状态:Http 是无状态的协议。所谓的无状态是指协议对于请求的处理没有记忆功
能。无状态意味着如果要再次处理先前的信息,则这些先前的信息必须要重传,这就导致
了数据量传输的增加。但是从另一方面来说,当先前的信息服务器不在使用的时候,则服
务器的响应将会非常的快。

### <a name="11>11. http 的安全问题。</a>
a、通信使用明文不加密,内容可能被窃听 <br>
b、不验证通信方身份,可能遭到伪装 <br>
c、无法验证报文完整性,可能被篡改 <br>
HTTPS 就是 HTTP 加上加密处理(一般是 SSL 安全通信线路)+认证+完整性保护

### <a name="12>12. Https 的作用。</a>
- 内容加密 建立一个信息安全通道,来保证数据传输的安全;
- 身份认证 确认网站的真实性
- 数据完整性 防止内容被第三方冒充或者篡改 <br>
[02_12_1](/data/images/Java应届生面试突击/计算机网络/02_12_1.png) <br>

### <a name="13>13. 浏览器和服务器在基于 https 进行请求链接到数据传输过程中,用到了哪些技术?</a>
1. 对称加密算法 <br>
用于对真正传输的数据进行加密。 <br>
2. 非对称加密算法 <br>
用于在握手过程中加密生成的密码。非对称加密算法会生成公钥和私钥,公钥只能用于
加密数据,因此可以随意传输,而网站的私钥用于对数据进行解密,所以网站都会非常小心的
保管自己的私钥,防止泄漏。 <br>
3. 散列算法 <br>
用于验证数据的完整性。 <br>
4. 数字证书 <br>
&ensp;&ensp;&ensp;&ensp;
    数字证书其实就是一个小的计算机文件,其作用类似于我们的身份证、护照,用于证明身
份,在 SSL 中,使用数字证书来证明自己的身份。 <br>
&ensp;&ensp;&ensp;&ensp;
    客户端有公钥,服务器有私钥,客户端用公钥对`对称密钥`进行加密,将加密后的对称密
钥发送给服务器,服务器用私钥对其进行解密,所以客户端和服务器可用对称密钥来进行通信。
公钥和私钥是用来加密密钥,而对称密钥是用来加密数据,分别利用了两者的优点。 <br>

### <a name="14>14. 讲下 Http 协议。</a>
&ensp;&ensp;&ensp;&ensp;
    主要包括 http 建立连接的过程,持久和非持久连接,带流水与不带流水,dns 解析过程,
get 和 post 区别,http 与 https 的区别等。状态码,Header 各个字段的意义。
http 和 socket 的区别,两个协议哪个更高效一点。 <br>
   
### <a name="15>15. http 和 socket 的区别,两个协议哪个更高效一点。</a>
&ensp;&ensp;&ensp;&ensp;
    创建 Socket 连接时,可以指定使用的传输层协议,Socket 可以支持不同的传输层协
议(TCP 或 UDP),当使用 TCP 协议进行连接时,该 Socket 连接就是一个 TCP 连接。
Socket 连接一旦建立,通信双方即可开始相互发送数据内容,直到双方连接断开。注意,
同 HTTP 不同的是 http 只能基于 tcp,socket 不仅能走 tcp,而且还能走 udp,这个是 socket
的第一个特点。 <br>
&ensp;&ensp;&ensp;&ensp;
    HTTP 连接使用的是“请求—响应”的方式,不仅在请求时需要先建立连接,而且需要
客户端向服务器发出请求后,服务器端才能回复数据。 <br>
&ensp;&ensp;&ensp;&ensp;
    很多情况下,需要服务器端主动向客户端推送数据,保持客户端与服务器数据的实时
与同步。此时若双方建立的是 Socket 连接,服务器就可以直接将数据传送给客户端;若双
方建立的是 HTTP 连接,则服务器需要等到客户端发送一次请求后才能将数据传回给客户
端。 <br>
&ensp;&ensp;&ensp;&ensp;
    Socket 效率高,至少不用解析 http 报文头部一些字段 。
    
### <a name="16>16. HTTP 与 HTTPS 的区别。</a>
●https 更安全 <br>
HTTPS 协议是由 SSL+HTTP 协议构建的可进行加密传输、身份认证的网络协议,
要比 http 协议安全,所有传输的内容都经过加密,加密采用对称加密,但对称加密的密钥用服务器
方的证书进行了非对称加密。http 是超文本传输协议,信息是明文传输,没有加密,通过
抓包工具可以分析其信息内容。 <br>
●https 需要申请证书 <br>
https 协议需要到 CA 申请证书,一般免费证书很少,需要交费。而常见的 http 协议则没
有这一项。 <br>
●端口不同 <br>
http 使用的是 80 端口,而 https 使用的是 443 端口。 <br>
●所在层次不同 <br>
HTTP 协议运行在 TCP 之上,HTTPS 是运行在 SSL/TLS 之上的 HTTP 协议,SSL/TLS 运行在
TCP 之上。 <br>



---
### 搬运工信息
Author:Jason Lou <br>
Email:vip.iotworld@gmail.com <br>
Blog:https://blog.csdn.net/qq_21508727 <br>
Github:https://github.com/JGPY/JavaGuideBooster <br>
---
