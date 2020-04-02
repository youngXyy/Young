### Http(超文本传输协议)  HyperText Transfer Protoco

- 超文本

  指的是Html，css，JavaScript和图片等，Http的出现就是为了接收和发布Html页面，后面经过不断的发展也可以用来接收一些音频、视频、文件等内容。

- 通信
  C/S架构（客户端与服务端）、B/S架构（浏览器与服务器）之间的通信有Http协议和Tcp/Ip协议族在内的其他众多协议。
  客户端：请求访问文本或图片等资源的一方。

  服务端：提供响应的一方。
  Http是基于客户端/服务端的架构模型。浏览器或其他任何的客户端都可以用Http，通过URL地址向Http服务器即Web服务器发送所有请求，Web服务器端在接收到请求后做出处理响应给对方，就是向客户端传响应的信息。

  通过发送信息（请求）和响应信息（响应）达成交易（通信）

  Ps：在使用Http协议时，一端是客户端，则另一方必定是服务器端。

  ![image-20200402145656494](C:\Users\young\AppData\Roaming\Typora\typora-user-images\image-20200402145656494.png)

- ------

  ### 特点

  支持客户端，服务端模式，简单快速，客户端向服务器请求服务时，只需传送请求方法和路径，灵活，HTTP允许传输任意类型的数据对象，无连接，限制每次连接只处理一个请求。无状态，Http协议是无状态协议，指定协议对于事务处理没有记忆能力。Http都是由客户端发起请求，并且由服务器端回应响应的消息。

  无状态：每一次的请求都是互相独立的，第一个请求与第二个请求也没有先后的顺序，也没有必要的联系。

  无连接：每次服务器在处理完客户端的请求后，并收到客户端的应答后，就断开了通信。客户端再次进行请求时又是创建了一个新的连接，采取这种方式是节省传输的时间。

- Http1.0 的缺点：Http是一种不保存状态，无状态协议，协议对于发送过来或者响应都不做持久化处理。的每个TCP连接只能发送一个请求，发送完数据后连接就关闭了，如果还要请求就必须要建立一个新的请求连接。

- Http1.1 虽然是无状态协议，但是为了实现期望的保持状态功能，引入了Cookie技术。Cookie和Http协议通信，就可以管理状态。

  ![image-20200402150921388](C:\Users\young\AppData\Roaming\Typora\typora-user-images\image-20200402150921388.png)

  ![image-20200402151049771](C:\Users\young\AppData\Roaming\Typora\typora-user-images\image-20200402151049771.png)

  Tcp的新建成本很高因为需要客户端和服务器进行三次握手。

  Http1.1可以持久连接，Tcp连接默认不关闭，可以被多个请求复用，只要在一段时间内，没有请求，就自动关闭。

- ### Http消息结构

  一个请求消息是由请求行，请求头字段，一个空行和消息主体（响应消息的承载数据）组成。

  客户端：发送请求

  ![image-20200402153009140](C:\Users\young\AppData\Roaming\Typora\typora-user-images\image-20200402153009140.png)

  服务器：发送响应

  ![image-20200402153017906](C:\Users\young\AppData\Roaming\Typora\typora-user-images\image-20200402153017906.png)

  ![image-20200402153059084](C:\Users\young\AppData\Roaming\Typora\typora-user-images\image-20200402153059084.png)

  **GET，Request Method，请求方法，Request URL，为请求的url的地址，Status Code为状态码，Remote Address为地址。**

- ### URI、URL、URN

  URI（统一资源标识符）,URL（统一资源定位符）,URN（统一资源名）是用来识别，定位和命名互联网上的资源。

  ![image-20200402153710617](C:\Users\young\AppData\Roaming\Typora\typora-user-images\image-20200402153710617.png)

- 请求方式

  GET 从指定资源请求数据

  POST 向指定资源提交要被处理的数据

  HEAD 读取资源的元数据

  PUT 用来传输文件

  DELETE 删除资源数据

  OPTIONS 读取资源多支持的所有请求方法

  TRACE 回显服务器收到额请求

  CONNECT 保留将来使用

  |          |                     GET                      |                  POST                   |
  | :------: | :------------------------------------------: | :-------------------------------------: |
  |   缓存   |                   能被缓存                   |               不能被缓存                |
  | 历史记录 |                     保留                     |                  保留                   |
  |   书签   |                     收藏                     |                 不收藏                  |
  | 长度限制 | GET请求向URL添加数据，URL长度限制在2048字符  |                 不限制                  |
  | 数据类型 |              只允许*ASC*II字符               |          没有限制，二进制数据           |
  |  安全性  | GET请求发送数据是URL的一部分，敏感数据不安全 | 比get安全，参数不会被保存在浏览器历史中 |
  |   可见   |           数据在URL中对所有人可见            |            数据不显示在URL中            |

  - 常见的状态码

    ![image-20200402170850460](C:\Users\young\AppData\Roaming\Typora\typora-user-images\image-20200402170850460.png)

- 工作原理

  ![image-20200402170933472](C:\Users\young\AppData\Roaming\Typora\typora-user-images\image-20200402170933472.png)