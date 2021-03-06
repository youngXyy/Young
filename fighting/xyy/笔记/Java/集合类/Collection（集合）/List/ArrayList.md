### ArrayList（数组列表）

ArrayList是数组列表，主要用来装载数据，当装载的是基本数据类型int，long，double，float，char，byte，Boolean，short。只能存储他们对应的包装类，它的主要底层实现是数组Object[] elementData。

为啥线程不安全还使用呢？

我们正常的使用场景中，大部分是用来查询的，不会涉及太频繁的增删。如果涉及频繁的增删，可以使用LinkedList，如果想线程安全的话使用Vector。这就是三者的区别。

不存在一个集合框架查询效率快，增删效率也高，还是线程安全的。以为数据结构的特性就是优劣共存的。

ArrayList 底层结构是动态数组结构，它对于对象的查询的时间复杂度是O（1），查询效率很快，查询是基于index下标直接查询数组，但在插入数据的时候因为会涉及到数组的移位复制（尾部插入除外）



#### 源码

get（）方法

```java
public E get(int index) {
    rangeCheck(index);

    return elementData(index);
}
```

//rangeCheck（）

```java
private void rangeCheck(int index) {
    if (index >= size)
        throw new IndexOutOfBoundsException(outOfBoundsMsg(index));
}

    E elementData(int index) {
        return (E) elementData[index];
    }
```

查询的时候会先判断是否index超过了数组的长度抛出异常。然后直接根据index查询