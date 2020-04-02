# 一个程序是怎么运行的

![image-20200330161217590](C:\Users\young\AppData\Roaming\Typora\typora-user-images\image-20200330161217590.png)

![image-20200330172307146](C:\Users\young\AppData\Roaming\Typora\typora-user-images\image-20200330172307146.png)

 

Constant pool(常量池)

JDK1.7中位于JVM的方法区中，JDK1.8后常量池存在于堆内存上，堆内存上共享数据，所以会存在线程安全问题。

元空间是在内存上开辟的一块地址，用于存放运行时常量池信息，例如String类的intern（）方法。



这些字节码通过字节码执行引擎去执行，之后Cpu将程序运行的结果通过地址总线将数据传输显示到设备上。