## TCP 三次握手

TCP 三次握手就好比两个人在街上隔着50米看见了对方，但是因为雾霾等原因不能100%确认，所以要通过招手的方式相互确定对方是否认识自己。张三首先向李四招手(**syn**)，李四看到张三向自己招手后，向对方点了点头挤出了一个微笑(**ack**)。张三看到李四微笑后确认了李四成功辨认出了自己(进入**estalished**状态)。

但是李四还有点狐疑，向四周看了一看，有没有可能张三是在看别人呢，他也需要确认一下。所以李四也向张三招了招手(**syn**)，张三看到李四向自己招手后知道对方是在寻求自己的确认，于是也点了点头挤出了微笑(**ack**)，李四看到对方的微笑后确认了张三就是在向自己打招呼(进入**established**状态)。

![img](https://mmbiz.qpic.cn/mmbiz_gif/bGribGtYC3mJebROaNfpaTGxauaAjuwU4ibTjbFMPeNfm2vJiaibmwb6AiasohkyvQyTLmyTl92h2dI53IM1U3t48hA/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

于是两人加快步伐，走到了一起，相互拥抱。![img](https://mmbiz.qpic.cn/mmbiz_gif/bGribGtYC3mJebROaNfpaTGxauaAjuwU4NMictk5alQyl0PHEZxzmCF1QRfYb9I2PicCocEh1O9gmJjhAdwqEILcA/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

我们可以看到这个过程中一共出现四个动作，张三招手---李四点头微笑---李四招手---张三点头微笑。一共四个动作，其中李四连续2个动作先是点头微笑，然后再次招手。实际上可以将这两个动作合一（syn+ack）。四个动作简化成3个就是张三招手-李四点头微笑并招手-张三点头微信。这就是三次握手的本质。

syn_send ---syn--> syn_rcvd   syn_rcvd--ack+syn--> syn_send(established)   syn_send--ack--->syn_rvcd (established已确定)

这边有两个中间状态 syn_send和syn_rvcd  这两个状态是【半打开】状态，就是向对方招手了，但还没来得及看到对方的点头和微笑。syn_send是主动打开方的【半打开】状态，syn_rcvd 是被动打开方的【半打开】状态。

### TCP数据传输

 TCP 数据传输就是两个人隔空对话，差了一点距离，所以需要对方反复确认听见了自己的话。



![img](https://mmbiz.qpic.cn/mmbiz_gif/bGribGtYC3mJebROaNfpaTGxauaAjuwU4iaKYGwQudgjaSpnw3mkl4MapuxeHI7UwibROoWnDvrfjFa2HQdHUjKWw/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

张三喊了一句话(data)，李四听见了之后要向张三回复自己听见了(ack)。

如果张三喊了一句，半天没听到李四回复，张三就认为自己的话被大风吹走了，李四没听见，所以需要重新喊话，这就是tcp重传。

也有可能是李四听到了张三的话，但是李四向张三的回复被大风吹走了，以至于张三没听见李四的回复。张三并不能判断究竟是自己的话被大风吹走了还是李四的回复被大风吹走了，张三也不用管，重传一下就是。

既然会重传，李四就有可能同一句话听见了两次，这就是「去重」。「重传」和「去重」工作操作系统的网络内核模块都已经帮我们处理好了，用户层是不用关心的![img](https://mmbiz.qpic.cn/mmbiz_gif/bGribGtYC3mJebROaNfpaTGxauaAjuwU4Y1NDpMzlBvxGuylksMBvMHWLlficSqZbkoF7WvBxQdB0AGBibSAvOaLA/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

### 四次挥手

TCP断开链接的过程和建立链接的过程比较类似，只不过中间的两部并不总是会合成一步走，所以它分成了4个动作，张三挥手(fin)——李四伤感地微笑(ack)——李四挥手(fin)——张三伤感地微笑(ack)。

![img](https://mmbiz.qpic.cn/mmbiz_gif/bGribGtYC3mJebROaNfpaTGxauaAjuwU48bR46gzNlsZXicxq8ZW4RrZJznhnwYibpiasgMQUcibmqVfYgdq1WHggUA/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

之所以中间的两个动作没有合并，是因为tcp存在「半关闭」状态，也就是单向关闭。张三已经挥了手，可是人还没有走，只是不再说话，但是耳朵还是可以继续听，李四呢继续喊话。等待李四累了，也不再说话了，超张三挥了挥手，张三伤感地微笑了一下，才彻底结束了。



中间有个非常特殊的状态，就是time_wait ，它是主动关闭的一方回复完对方的挥手后进入的一个长期的状态这个长期的状态持续时间是4分钟，4分钟后会进入close状态。释放套接字资源。具体实现这个时间是可以修改的。它作用是重传最后一个ack报文。如果对方没有收到ack话，会重传fin报文，处于time_wait状态的套接字会立即向对方重发ack。这段期间，该连接在对话期间于于网际路由上产生的残留报文（因为路径过于崎岖，数据报文走的时间太长，重传的报文都收到了，原始报文还在路上）传过来时，都会被立即丢弃掉。4分钟的时间足以使得这些残留报文彻底消逝。不然当新的端口被重复利用时，这些残留报文可能会干扰新的链接。

为什么是4分钟，4分钟是2给MSL（Max segment lifetime ）--最长报文寿命。这个时间是由官方RFC协议规定的。至于为什么是2给MSL而不是1个，emmm。。。这里骚羊也不能合理解释。

四次挥手也并不是总是四次挥手，中间的两个动作有时候是可以合并一起进行的，就成了三次挥手，主动关闭方就会从fin_wait_1状态直接进入time_wait状态，跳过了fin_wait_2状态。



