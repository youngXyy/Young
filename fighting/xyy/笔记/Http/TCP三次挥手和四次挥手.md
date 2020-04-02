## TCP 三次握手

TCP 三次握手就好比两个人在街上隔着50米看见了对方，但是因为雾霾等原因不能100%确认，所以要通过招手的方式相互确定对方是否认识自己。张三首先向李四招手(**syn**)，李四看到张三向自己招手后，向对方点了点头挤出了一个微笑(**ack**)。张三看到李四微笑后确认了李四成功辨认出了自己(进入**estalished**状态)。

但是李四还有点狐疑，向四周看了一看，有没有可能张三是在看别人呢，他也需要确认一下。所以李四也向张三招了招手(**syn**)，张三看到李四向自己招手后知道对方是在寻求自己的确认，于是也点了点头挤出了微笑(**ack**)，李四看到对方的微笑后确认了张三就是在向自己打招呼(进入**established**状态)。

![img](https://mmbiz.qpic.cn/mmbiz_gif/bGribGtYC3mJebROaNfpaTGxauaAjuwU4ibTjbFMPeNfm2vJiaibmwb6AiasohkyvQyTLmyTl92h2dI53IM1U3t48hA/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

于是两人加快步伐，走到了一起，相互拥抱。![img](https://mmbiz.qpic.cn/mmbiz_gif/bGribGtYC3mJebROaNfpaTGxauaAjuwU4NMictk5alQyl0PHEZxzmCF1QRfYb9I2PicCocEh1O9gmJjhAdwqEILcA/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)