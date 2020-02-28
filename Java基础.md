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