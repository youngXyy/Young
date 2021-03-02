# 你真的了解你写的代码是怎么运行的吗？

###### Every Old 铁，我是骚羊羊，一个生存在互联网最低端的男银！

------

> `首先，要成为Java王者，那骚瑞肯定了解Java程序是怎么去运行的呀！话不多BB，下面骚羊来讲解（此处应有掌声PPP）` 
>
> Java代码有很多运行的方式
>
> - 在开发工具中运行
> - 双击jar文件运行
> - 在命令行中运行
> - 在网页中运行

- [ ] #### 跨平台运行


Java作为一门高级程序语言，它的语法复杂，抽象程度也高。因此在硬件上直接运行java并不现实。所以就需要一个虚拟机来托管环境（也就是我们熟悉的JVM虚拟机）这个环境可以帮我们处理一些代码中冗长且容易出错的部分。还能自动内存管理与垃圾回收。当然更多的时候还是在各个平台提供软件的实现，这样一旦一个程序被编译成Java字节码，那么它就可以在不同的虚拟机实现运行。主要系统有Jvm运行环境，Java代码就可以运行，这也就是Java的跨平台性。

------

- [ ] ##### 我们写的Java文件，都是经过javac编译器编译生成.class文件才能被JVM识别。我们平时见的.jar文件其实就是.class文件的压缩包，被加载到JVM才可以运行。

- 先来编写一段入门级代码(用粘贴到记事本)

  ```java
  public class Hello {
  	public static void main(String[] args){
  		boolean flag = true;
  		if(flag)
  			System.out.println("Hello, Java!!");
  		if(flag == true)
  			System.out.println("Hello, JVM!!!");
  	}
  }
  ```

然后执行

```shell
javac Hello.java   java Hello
```

查看结果。

![image-20200626171102451](D:\Work\Young\img\image-20200626171102451.png)

执行 

```shell
javap -c -s Hello.class
```

查看反编译程序

![image-20200626180947304](D:\Work\Young\img\image-20200626180947304.png)



- [ ] #### 了解下Java是怎么运行Java字节码的？

  ![img](D:\Work\Young\img\webp.png)

  [^记小本本]: .java文件通过javac编译为.class文件经过类加载、执行引擎、运行数据区以及垃圾回收器

  

![image-20200626182346906](D:\Work\Young\img\image-20200626182346906.png)

Constant pool(常量池)

JDK1.7中位于JVM的方法区中，JDK1.8后常量池存在于堆内存上，堆内存上共享数据，所以会存在线程安全问题。

元空间是在内存上开辟的一块地址，用于存放运行时常量池信息，例如String类的intern（）方法。



这些字节码通过字节码执行引擎去执行，之后Cpu将程序运行的结果通过地址总线将数据传输显示到设备上。