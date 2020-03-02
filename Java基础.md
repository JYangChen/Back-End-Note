# Java基础



## 封装 继承 多态

- **覆盖/重写**

- **重载**

- **向上转型**

  ```java
  Father f = new Son();
  ```

  

- **强制向下转型**

  父类必须实际指向了一个子类对象才可强制类型向下转型

  ```java
  Father f = new Son();
  Son s = (Son)f;
  ```



## 抽象类和接口



### 区别

- 抽象类中可以没有抽象方法，也可以抽象方法和非抽象方法共存
- 接口中的方法在JDK8之前只能是抽象的，JDK8版本开始提供了接口中方法的default实现
- 抽象类和类一样是单继承的；接口可以实现多个父接口
- 抽象类中可以存在普通的成员变量；接口中的变量必须是static final类型的，必须被初始化，接口中只有常量，没有变量

### 使用情况

- 当需要定义一些抽象方法而不需要其余额外的具体方法或者变量的时候，我们可以使用接口；反之，则需要使用抽象类



## Java中的8种基本数据类型及其取值范围

- byte：1字节
- short：2字节
- int：4个字节
- long：8字节
- float：4字节
- double：8字节
- char：2字节

- boolean：Java规范中并没有规定boolean类型所占字节数
- int的取值范围为 Integer.MIN_VALUE 到 Integer.MAX_VALUE



## 元注解

**作用**:负责注解其它注解



### Target

- 说明注解所修饰的对象范围

- ```java
  public enum ElementType { 
    TYPE,FIELD,METHOD,PARAMETED,CONSTRUCTOR,LOCAL_VARIABLE,ANNOCATION_TYPE,PACKAGE,TYPE_PARAMETER,TYPE_USE 
  } 
  @Target({ElementType.TYPE, ElementType.METHOD}) 
  ```

  

### Retention（保留策略）

- 定义了该注解被保留的时间长短

- ```java
  public enum RetentionPolicy { 
      SOURCE, CLASS, RUNTIME 
  }
  //SOURCE：表示在源文件中有效（即源文件保留）
  //CLASS：表示在class文件中有效（即class保留）
  //RUNTIME：表示在运行时有效（即运行时保留）
  @Retention(RetentionPolicy.RUNTIME)
  ```



###  Documented

- 描述其它类型的annotation应该被作为被标注的程序成员的公共API，因此可以被javadoc此类的工具文档化，是一个标记注解，没有成员



### Inherited

- 是一个标记注解，@Inherited阐述了某个被标注的类型是被继承的。如果一个使用了@Inherited修饰的annotation类型被用于一个class，则这个annotation将被用于该class的子类



## 反射机制



### 定义

- **反射机制**是指在运行中，对于任意一个类，都能够知道这个类的所有属性和方法。对于任意一个对象，都能够调用它的任意一个方法和属性。即**动态获取信息和动态调用对象方法的功能**称为反射机制。



### 作用

- 在运行时判断任意一个对象所属的类
- 在运行时构造一个类的对象
- 在运行时判断任意一个类所具有的成员变量和方法
- 在运行时调用任意一个对象的方法，生成动态代理



### 相关的类

- **Class：表示类**，用于获取类的相关信息
- **Field：表示成员变量**，用于获取实例变量和静态变量等
- **Method：表示方法**，用于获取类中的方法参数和方法类型等
- **Constructor：表示构造器**，用于获取构造器的相关参数和类型等



## 异常



### Exception和Error的区别

- **Exception**是程序正常运行中**预料到可能会出现**的错误，并且应该被捕获并进行相应的处理，是一种**异常**现象
- **Error**是正常情况下不可能发生的错误，**Error会导致JVM处于一种不可恢复的状态**，不需要捕获处理，比如说OutOfMemoryError



## 值传递和引用传递

- **值传递，**意味着传递了对象的一个副本，即使副本被改变，也不会影响源对象。
- **引用传递，**意味着传递的并不是实际的对象，而是对象的引用。因此，外部对引用对象的改变会反映到所有的对象上。



## 三大集合



### 常见集合

Java中的常见集合可以概括如下。

- **Map接口和Collection接口是所有集合框架的父接口**
- Collection接口的子接口包括：Set接口和List接口
- Map接口的实现类主要有：**HashMap**、TreeMap、Hashtable、LinkedHashMap、**ConcurrentHashMap**以及Properties等
- Set接口的实现类主要有：HashSet、TreeSet、LinkedHashSet等
- List接口的实现类主要有：**ArrayList**、**LinkedList**、Stack以及Vector等



### HashMap和Hashtable的区别

HashMap和Hashtable之间的区别可以总结如下。

- HashMap没有考虑同步，是线程不安全的；Hashtable使用了synchronized关键字，是线程安全的；
- HashMap允许null作为Key；Hashtable不允许null作为Key，Hashtable的value也不可以为null



### 快速失败（fast-fail）机制

- HashMap和Hashtable都有fast-fail（Hashtable本身虽然线程安全,但是对Hashtable返回的任何形式collection使用Iterator都是会快速失败的）。
- 快速失败是Java集合的一种**错误检测机制**，当多个线程对集合进行结构上的改变的操作时，**有可能**会产生fail-fast。

- 异常的抛出条件是检测到 modCount != expectedmodCount。
- 场景：java.util包下的集合类都是快速失败的，不能在多线程下发生并发修改（迭代过程中被修改）。



### 安全失败（fail—safe）机制

- 原理：迭代时是对原集合的拷贝进行遍历。
- 场景：java.util.concurrent包下的容器都是安全失败，可以在多线程下并发使用，并发修改。



### HashMap

- 底层实现：HashMap底层实现数据结构为**数组+链表**的形式，JDK8及其以后的版本中使用了**数组+链表+红黑树**实现，解决了链表太长导致的查询速度变慢的问题。

- HashMap的初始容量16，加载因子为0.75，扩容增量是原容量的1倍。如果HashMap的容量为16，一次扩容后容量为32。HashMap扩容是指元素个数**（包括数组和链表+红黑树中）**超过了16*0.75=12之后开始扩容。
- 将一个键值对插入HashMap中，通过**将Key的hash值与length-1进行&运算**，实现了当前Key的定位，2的幂次方的容量可以减少冲突（碰撞）的次数，提高HashMap查询效率。



## Java 内存模型



### Java回收算法

- 标记-复制算法
- 标记-清理
- 标记-整理



## Object类方法



### clone方法

保护方法，实现对象的浅复制，只有实现了Cloneable接口才可以调用该方法，否则抛出CloneNotSupportedException异常。

主要是JAVA里除了8种基本类型传参数是值传递，其他的类对象传参数都是引用传递，我们有时候不希望在方法里讲参数改变，这是就需要在类中复写clone方法。

### getClass方法

final方法，获得运行时类型。

### toString方法

该方法用得比较多，一般子类都有覆盖。

### finalize方法

该方法用于释放资源。因为无法确定该方法什么时候被调用，很少使用。

### equals方法

该方法是非常重要的一个方法。一般equals和==是不一样的，但是在Object中两者是一样的。子类一般都要重写这个方法。

### hashCode方法

该方法用于哈希查找，可以减少在查找中使用equals的次数，重写了equals方法一般都要重写hashCode方法。这个方法在一些具有哈希功能的Collection中用到。

一般必须满足obj1.equals(obj2)==true。可以推出obj1.hash- Code()==obj2.hashCode()，但是hashCode相等不一定就满足equals。不过为了提高效率，应该尽量使上面两个条件接近等价。

如果不重写hashcode(),在HashSet中添加两个equals的对象，会将两个对象都加入进去。

### wait方法

wait方法就是使当前线程等待该对象的锁，当前线程必须是该对象的拥有者，也就是具有该对象的锁。wait()方法一直等待，直到获得锁或者被中断。wait(long timeout)设定一个超时间隔，如果在规定时间内没有获得锁就返回。

调用该方法后当前线程进入睡眠状态，直到以下事件发生。

- 其他线程调用了该对象的notify方法。

- 其他线程调用了该对象的notifyAll方法。

- 其他线程调用了interrupt中断该线程。

- 时间间隔到了。

此时该线程就可以被调度了，如果是被中断的话就抛出一个InterruptedException异常。

### notify方法

该方法唤醒在该对象上等待的某个线程。

### notifyAll方法

该方法唤醒在该对象上等待的所有线程。

### finalize()

- ### 作用

  Java允许在类中定义一个名为finalize()的方法。它的工作原理是：一旦垃圾回收器准备好释放对象占用的存储空间，将首先调用其finalize()方法。并且在下一次垃圾回收动作发生时，才会真正回收对象占用的内存。

  关于垃圾回收，有三点需要记住：

  - 对象可能不被垃圾回收。只要程序没有濒临存储空间用完的那一刻，对象占用的空间就总也得不到释放。
  - 垃圾回收并不等于“析构”。
  - 垃圾回收只与内存有关。使用垃圾回收的唯一原因是为了回收程序不再使用的内存。

- ### 用途
  无论对象是如何创建的，垃圾回收器都会负责释放对象占据的所有内存。这就将对finalize()的需求限制到一种特殊情况，即通过某种创建对象方式以外的方式为对象分配了存储空间。不过这种情况一般发生在使用“本地方法”的情况下，本地方法是一种在Java中调用非Java代码的方式。

- ### 为什么不能显示直接调用finalize方法？
   如前文所述，finalize方法在垃圾回收时一定会被执行，而如果在此之前显示执行的话，也就是说finalize会被执行两次以上，而在第一次资源已经被释放，那么在第二次释放资源时系统一定会报错，因此一般finalize方法的访问权限和父类保持一致，为protected。