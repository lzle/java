## 目录

* [环境](#环境)
    * [安装](#安装)
    * [Hello World](#hello-world)
* [修饰符](#修饰符)
    * [default](#default)
    * [private](#private)
    * [public](#public)
    * [protected](#protected)
    * [static](#static)
    * [final](#final)
    * [abstract](#abstract)
    * [synchronized](#synchronized)
* [流程控制](#流程控制)
    * [while](#while)
    * [do while](#do-while)
    * [for](#for)
    * [break](#break)
    * [continue](#continue)
    * [if else](#if-else)
    * [switch case](#switch-case)
* [类](#类)
    * [构造方法](#构造方法)
    * [继承](#继承)
    * [重写](#重写)
    * [重载](#重载)
    * [多态](#多态)
    * [多态](#多态)
    * [抽象](#抽象)
    * [封装](#封装)
    * [接口](#接口)
    * [枚举](#枚举)




## 环境
Java是一种广泛使用的编程语言，具有跨平台、面向对象、安全性高等特点。它最初由Sun Microsystems公司于1995年发布，现在属于Oracle公司。Java可以用于开发各种应用程序，包括桌面应用程序、网站后端、移动应用程序(Android)、嵌入式系统等。Java的核心理念是“一次编写，到处运行”，这得益于Java虚拟机（JVM）的架构，使得Java编写的程序可以在任何支持JVM的平台上运行而无需重新编译。Java是一种静态类型、编译型语言，同时也支持自动垃圾回收，减轻了内存管理的负担。

### 安装
Java的安装分为两个部分：JDK（Java Development Kit）和JRE（Java Runtime Environment）。JDK包含了Java的开发工具，如javac、java等，JRE包含了Java的运行环境，用于运行Java程序。在安装Java之前，需要先安装JDK，然后再安装JRE。以下是在CentOS上安装Java的步骤：

#### 方法 1：通过 yum 安装

查看 yum 库支持的 Java 版本

```bash
$ yum search java|grep jdk
```

选择版本安装 jdk

```bash
$ yum install java-1.8.0-openjdk
$ yum install java-1.8.0-openjdk-devel
```

验证是否安装成功

```bash
$ java -version
openjdk version "1.8.0_412"
OpenJDK Runtime Environment (build 1.8.0_412-b08)
OpenJDK 64-Bit Server VM (build 25.412-b08, mixed mode)
```

#### 方法 2：通过源码安装

从 [官网](https://www.oracle.com/cn/java/technologies/javase-downloads.html) 获取安装包, 使用 wget 命令下载

```bash
$ mkdir /usr/local
$ cd /usr/local
$ wget https://download.oracle.com/otn/java/jdk/8u202-b08/1961070e4c9b4e26a04e7f5a083f551e/jdk-8u202-linux-x64.tar.gz?AuthParam=1718551424_b71ec810b7f4719651ac8dfd4ad35cf9
$ tar -zxvf jdk-8u202-linux-x64.tar.gz
```

配置环境变量

```bash
$ vim /etc/profile
export JAVA_HOME=/usr/local/jdk1.8.0_202
export JRE_HOME=$JAVA_HOME/jre
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
$ source /etc/profile
```

验证是否安装成功

```bash
$ java -version
java version "1.8.0_202"
Java(TM) SE Runtime Environment (build 1.8.0_202-b08)
Java HotSpot(TM) 64-Bit Server VM (build 25.202-b08, mixed mode)
```

### Hello World

测试文件 HelloWorld.java

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

执行文件

```
$ javac HelloWorld.java
$ java HelloWorld
Hello World
```

## 修饰符

修饰符是 `Java` 中用于控制类、方法、变量等访问权限和行为的关键字。它们可以分为访问修饰符和非访问修饰符两大类。

### default

`default` 表示默认，什么也不写，在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。

如果在类、变量、方法或构造函数的定义中没有指定任何访问修饰符，那么它们就默认具有默认访问修饰符。

默认访问修饰符的访问级别是包级别，即只能被同一包中的其他类访问。

如下例所示，变量和方法的声明可以不使用任何修饰符。

```java
// MyClass.java
 
class MyClass {  // 默认访问修饰符
 
    int x = 10;  // 默认访问修饰符
 
    void display() {  // 默认访问修饰符
        System.out.println("Value of x is: " + x);
    }
}
 
// MyOtherClass.java
 
class MyOtherClass {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        obj.display();  // 访问 MyClass 中的默认访问修饰符变量和方法
    }
}
```

以上实例中，`MyClass` 类和它的成员变量 x 和方法 `display()` 都使用默认访问修饰符进行了定义。`MyOtherClass` 类在同一包中，因此可以访问 `MyClass` 类和它的成员变量和方法。

`default` 与 `protected` 的区别在于，`protected` 访问修饰符允许子类访问父类的成员变量和方法，即使它们不在同一包中。而 `default` 访问修饰符只允许同一包中的类（子类）访问。


### private

在 `Java` 中，`private` 是最严格的访问控制修饰符，用于实现封装。它限定成员只能在 声明它的类内部被访问，外部包括子类和同包的其他类都无法访问。使用对象：变量、方法。

```java
public class Logger {
   private String format;
   public String getFormat() {
      return this.format;
   }
   public void setFormat(String format) {
      this.format = format;
   }
}
```

`private` 访问修饰符的使用主要用来隐藏类的实现细节和保护类的数据。

### public

在 `Java` 中，`public` 是访问权限最大的修饰符，表示可以被任何其他类访问，不受包和继承关系的限制。使用对象：类、接口、变量、方法

被声明为 `public` 的类、方法、构造方法和接口能够被任何其他类访问。

如果几个相互访问的 `public` 类分布在不同的包中，则需要导入相应 `public` 类所在的包。由于类的继承性，类所有的公有方法和变量都能被其子类继承。

```java
// 文件：people/Person.java
package people;

public class Person {
    public String name = "Alice";       // public 字段

    public void sayHello() {            // public 方法
        System.out.println("Hello, I'm " + name);
    }
}

// 文件：test/TestPerson.java
package test;

import people.Person;

public class TestPerson {
    public static void main(String[] args) {
        Person p = new Person();
        System.out.println(p.name);    // 合法访问 public 字段
        p.sayHello();                  // 合法访问 public 方法
    }
}
```

### protected

在 `Java` 中，`protected` 是一种访问修饰符，使用对象：变量、方法，用于控制类成员（属性、方法、构造器）的可见性。
它的访问范围介于 `private` 和 `public` 之间，具体如下：

`protected` 的访问范围：

1. **同一包内的类**：`protected` 成员可以被同一包内的其他类访问。

2. **子类**：`protected` 成员可以被任何子类访问，无论子类是否在同一包内。

3. **不同包的非子类**：`protected` 成员不能被不同包内的非子类访问。

测试目录结构

```
src/
├── a/
│   ├── Base.java
│   ├── A1.java
│   └── A2.java
└── b/
    ├── B1.java
    └── B2.java
```

测试文件 `Base.java`

```java
package a;

public class Base {
    protected String msg = "protected value";

    protected void sayHello() {
        System.out.println("Base says: " + msg);
    }
}
```

测试文件 `A1.java`, 同包非继承。

```java
package a;

public class A1 {
    public static void main(String[] args) {
        Base base = new Base();
        System.out.println(base.msg); 
        base.sayHello();   
        
        // sayHello(); // The method sayHello() is undefined for the type A1
        // System.out.println(msg); // msg cannot be resolved to a variable
    }
    
    // public void bark() {
    //     System.out.println(msg); // The method sayHello() is undefined for the type A1
    //     sayHello(); // msg cannot be resolved to a variable
    // }
}
```

测试文件 `A2.java`，同包继承。

```java
package a;

public class A2 extends Base {
    public static void main(String[] args) {
        A2 obj = new A2();
        System.out.println(obj.msg); 
        obj.sayHello();

        // System.out.println(msg); // Cannot make a static reference to the non-static field msg
        // sayHello(); // Cannot make a static reference to the non-static method sayHello() from the type A2

        Base base = new Base();
        System.out.println(base.msg);
        base.sayHello(); // OK
    }

    public void bark() {
        // 这里可以访问父类的 protected 方法
        System.out.println(msg);
        sayHello(); // OK
    }
}
```

测试文件 `B1.java`，不同包非继承。

```java
package b;

import a.Base;

public class B1 {
    public static void main(String[] args) {
        Base base = new Base(); 
        // System.out.println(base.msg); // The field Base.msg is not visible
        // base.sayHello();              // The method sayHello() from the type Base is not visible
    }
}
```

测试文件 `B2.java`，不同包继承。

```java
package b;

import a.Base;

public class B2 extends Base {
    public static void main(String[] args) {
        B2 obj = new B2();
        System.out.println(obj.msg); 
        obj.sayHello();              

        // System.out.println(msg); // Cannot make a static reference to the non-static field msg
        // sayHello(); // Cannot make a static reference to the non-static method sayHello() from the type A2

        // 无法通过父类对象访问
        // Base base = new Base();
        // System.out.println(base.msg); // The field Base.msg is not visible
        // base.sayHello();              // The method sayHello() from the type Base is not visible
    }

    public void bark() {
        // 这里可以访问父类的 protected 方法
        System.out.println(msg); // OK
        sayHello();              // OK
    }
}
```

### static

`static` 是一个非访问修饰符，用于表示类的成员（变量和方法）属于类本身，用来修饰类方法和类变量。

**静态变量**：`static` 关键字用来声明独立于对象的静态变量，无论一个类实例化多少对象，它的静态变量只有一份拷贝。
静态变量也被称为类变量。局部变量不能被声明为 `static` 变量。

**静态方法**：`static` 关键字用来声明独立于对象的静态方法。静态方法不能使用类的非静态变量。静态方法从参数列表得到数据，然后计算这些数据。

```java
public class InstanceCounter {
    private static int numInstances = 0;
    protected static int getCount() {
       return numInstances;
    }
  
    private static void addInstance() {
       numInstances++;
    }
  
    InstanceCounter() {
       InstanceCounter.addInstance();
    }
  
    public static void main(String[] arguments) {
       System.out.println("Starting with " +
       InstanceCounter.getCount() + " instances");
       for (int i = 0; i < 500; ++i){
         InstanceCounter.addInstance();
         new InstanceCounter();
      }
       System.out.println("Created " +
       InstanceCounter.getCount() + " instances");
    }
 }
```
输出结果：

```
Starting with 0 instances
Created 1000 instances
```


### final

`final` 表示"最后的、最终的"含义，变量一旦赋值后，不能被重新赋值。被 `final` 修饰的实例变量必须显式指定初始值。

`final` 修饰符通常和 `static` 修饰符一起使用来创建类常量。

```java
public class Test{
  final int value = 10;
  // 下面是声明常量的实例
  public static final int BOXWIDTH = 6;
  static final String TITLE = "Manager";
 
  public void changeValue(){
     value = 12; //将输出一个错误
  }
}
```

父类中的 final 方法可以被子类继承，但是不能被子类重写。声明 final 方法的主要目的是防止该方法的内容被修改。

```java
public class Test{
    public final void changeName(){
       // 方法体
    }
}
```

### abstract

抽象类不能用来实例化对象，声明抽象类的唯一目的是为了将来对该类进行扩充。

一个类不能同时被 `abstract` 和 `final` 修饰。如果一个类包含抽象方法，那么该类一定要声明为抽象类，否则将出现编译错误。

抽象类可以包含抽象方法和非抽象方法。

```java
abstract class Caravan{
   private double price;
   private String model;
   private String year;
   public abstract void goFast(); //抽象方法
   public abstract void changeColor();
}
```

抽象方法是一种没有任何实现的方法，该方法的具体实现由子类提供。

抽象方法不能被声明成 `final` 和 `static`。

任何继承抽象类的子类必须实现父类的所有抽象方法，除非该子类也是抽象类。

如果一个类包含若干个抽象方法，那么该类必须声明为抽象类。抽象方法的声明以分号结尾。

```java
public abstract class SuperClass{
    abstract void m(); //抽象方法
}
 
class SubClass extends SuperClass{
     //实现抽象方法
      void m(){
          .........
      }
}
```

### synchronized

`synchronized` 关键字声明的方法同一时间只能被一个线程访问。


## 流程控制

### while

`while` 循环是 `Java` 中的一种循环控制结构，用于在满足特定条件时重复执行一段代码。它的基本语法如下：

```java
while( 布尔表达式 ) {
  //循环内容
}
```

`while` 循环的执行过程如下：

```java
public class Test {
   public static void main(String[] args) {
      int x = 10;
      while( x < 20 ) {
         System.out.print("value of x : " + x );
         x++;
         System.out.print("\n");
      }
   }
}
```

### do while

`do while` 循环是 `Java` 中的一种循环控制结构，与 `while` 循环类似，但它至少会执行一次循环体。它的基本语法如下：

```java
do {
  //循环内容
} while( 布尔表达式 );
```

`do while` 循环的执行过程如下：

```java
public class Test {
   public static void main(String[] args){
      int x = 10;
 
      do{
         System.out.print("value of x : " + x );
         x++;
         System.out.print("\n");
      }while( x < 10 );
   }
}

// 输出结果
// value of x : 10
```

### for

`for` 循环是 `Java` 中的一种循环控制结构，用于在满足特定条件时重复执行一段代码。它的基本语法如下：

```java
for (初始化; 布尔表达式; 更新) {
  //循环内容
}
```

`for` 循环的执行过程如下：

```java
public class Test {
   public static void main(String[] args) {
 
      for(int x = 10; x < 20; x = x+1) {
         System.out.print("value of x : " + x );
         System.out.print("\n");
      }
   }
}
```

### break

`break` 主要用在循环语句或者 `switch` 语句中，用来跳出整个语句块。

### continue

`continue` 主要用在循环语句中，用来跳过当前循环的剩余部分，直接进入下一次循环。

### if else

`if else` 语句是 `Java` 中的一种条件控制结构。

```java
public class Test {
   public static void main(String args[]){
      int x = 30;
      if( x == 10 ){
         System.out.print("Value of X is 10");
      }else if( x == 20 ){
         System.out.print("Value of X is 20");
      }else if( x == 30 ){
         System.out.print("Value of X is 30");
      }else{
         System.out.print("这是 else 语句");
      }
   }
}
```

### switch case

`switch case` 执行时，一定会先进行匹配，匹配成功返回当前 `case` 的值，再根据是否有 `break`，判断是否继续输出。

```java
public class Test {
   public static void main(String args[]){
      //char grade = args[0].charAt(0);
      char grade = 'B';
 
      switch(grade)
      {
         case 'A' :
            System.out.println("优秀"); 
            break;
         case 'B' :
         case 'C' :
            System.out.println("良好");
         case 'D' :
            System.out.println("及格");
            break;
         case 'F' :
            System.out.println("你需要再努力努力");
            break;
         default :
            System.out.println("未知等级");
      }
      System.out.println("你的等级是 " + grade);
   }
}

// 良好
// 及格
// 你的等级是 B
```

如果当前匹配成功的 `case` 语句块没有 `break` 语句，则从当前 `case` 开始，后续所有 `case` 的值都会输出。

```java
public class Test {
   public static void main(String args[]){
      int i = 2;
      switch(i){
         case 0:
            System.out.println("0");
         case 1:
            System.out.println("1");
         case 2:
            System.out.println("2");
         default:
            System.out.println("default");
      }
   }
}

// 2
// default
```

如果都不匹配走 `default`，如果没有 `default` 语句，则不执行任何语句。


## 类

### 构造方法

在 `Java` 中，构造方法（Constructor）是用于创建类的对象的特殊方法。当使用 `new` 关键字创建对象时，构造方法会自动调用，用来初始化对象的属性。

构造方法具有以下几个特点：

* 与类名相同：构造方法的名称必须与类名完全一致，包括大小写。这是构造方法的一个基本要求。

* 没有返回类型：构造方法没有返回类型声明，即使是 void 也不写。这使得它与普通方法区分开来。

* 自动调用：每次使用 new 创建对象时，构造方法会自动调用，以初始化对象的属性和状态。

* 不能直接调用：构造方法只能通过 new 关键字在创建对象时调用，不能像普通方法那样直接调用。

* 支持重载：可以为一个类定义多个构造方法，只要它们的参数列表不同。通过重载，可以创建不同的构造方法以适应不同的初始化需求。

* 默认构造方法：如果没有定义任何构造方法，Java 会提供一个无参的默认构造方法。但一旦定义了任何其他构造方法，Java 不再提供默认构造方法。

* this 关键字的使用：在构造方法中可以使用 this 来引用当前对象的属性、方法，或调用另一个构造方法（必须是构造方法的第一行），以避免重复代码。

* 不能被继承，但可以被调用：构造方法不能被子类继承，但子类可以使用 super() 来调用父类的构造方法，以便初始化继承的属性。

* 对象初始化保障：构造方法的主要作用是初始化对象的属性和状态，保证对象在创建时处于一个合法的初始状态。

#### 构造方法的类型

1、无参构造方法（默认构造方法）

如果一个类中没有定义任何构造方法，Java 会默认提供一个无参构造方法。例如：

```java
public class Person {
    public Person() {
        System.out.println("Person对象已创建");
    }
}
```

2、有参构造方法

可以定义带有参数的构造方法，用来在创建对象时为属性赋值：

```java
public class Person {
    String name;
    int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

调用有参构造方法时，可以为对象的属性进行初始化：

```java
Person p = new Person("Alice", 25);
```

#### 构造方法的重载

Java 支持构造方法的重载，即可以在同一个类中定义多个构造方法，只要参数列表不同即可。例如：

```java
public class Person {
    String name;
    int age;

    public Person() {
        this.name = "Unknown";
        this.age = 0;
    }

    public Person(String name) {
        this.name = name;
        this.age = 0;
    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

创建对象时，Java 会根据传入的参数数量和类型自动选择匹配的构造方法：

```java
Person p1 = new Person(); // 调用无参构造方法
Person p2 = new Person("Alice"); // 调用单参数构造方法
Person p3 = new Person("Bob", 30); // 调用双参数构造方法
```

#### 构造方法中的 this 关键字

在构造方法中，`this` 关键字通常用于两种情况：

1、引用当前对象的属性或方法：当构造方法的参数名与类属性名相同时，使用 `this` 来区分类属性和参数。例如：

```java
public Person(String name, int age) {
    this.name = name; // this.name 表示类的属性
    this.age = age;
}
```

2、调用另一个构造方法：可以使用 this() 调用当前类的其他构造方法，常用于避免重复代码，但必须放在构造方法的第一行。

```java
public Person(String name) {
    this(name, 0); // 调用另一个双参数的构造方法
}

public Person(String name, int age) {
    this.name = name;
    this.age = age;
}
```

构造方法是 `Java` 面向对象编程中非常重要的部分，通过使用构造方法可以有效控制对象的初始化过程，保证创建出的对象状态的完整性和一致性。


### 继承

在 `Java` 中通过 `extends` 关键字可以申明一个类是从另外一个类继承而来的，一般形式如下：

```java
class 父类 {
}
 
class 子类 extends 父类 {
}
```

继承的特性:

* 子类拥有父类非 `private` 的属性、方法;

* 子类可以拥有自己的属性和方法，即子类可以对父类进行扩展;

* 子类可以重写父类的方法，即子类可以对父类的方法进行修改;

#### super 与 this

**super**：我们可以通过 `super` 关键字来实现对父类成员的访问，用来引用当前对象的父类。

**this**：指向自己的引用，引用当前对象，即它所在的方法或构造函数所属的对象实例。

```java
class Animal {
    void eat() {
        System.out.println("animal : eat");
    }
}
 
class Dog extends Animal {
    void eat() {
        System.out.println("dog : eat");
    }
    void eatTest() {
        this.eat();   // this 调用自己的方法
        super.eat();  // super 调用父类方法
    }
}
 
public class Test {
    public static void main(String[] args) {
        Animal a = new Animal();
        a.eat();
        Dog d = new Dog();
        d.eatTest();
    }
}
```

输出结果为：

```
animal : eat
dog : eat
animal : eat
```

#### 子类构造器

子类是不继承父类的构造器（构造方法或者构造函数）的，它只是调用（隐式或显式）。如果父类的构造器带有参数，
则必须在子类的构造器中显式地通过 `super` 关键字调用父类的构造器并配以适当的参数列表。

如果父类构造器没有参数，则在子类的构造器中不需要使用 `super` 关键字调用父类构造器，系统会自动调用父类的无参构造器。

需要注意的是父类中 `private` 字段如何在子类中访问和修改。

```java
class SuperClass {
    private int n;

    // 无参数构造器
    public SuperClass() {
        System.out.println("SuperClass()");
    }

    // 带参数构造器
    public SuperClass(int n) {
        System.out.println("SuperClass(int n)");
        this.n = n;
    }

    public int getN() {
        return n;
    }

    public void setN(int n) {
        this.n = n;
    }
}

class SubClass extends SuperClass {
    
    // 无参数构造器，自动调用父类的无参数构造器
    public SubClass() {
        System.out.println("SubClass()");
    }

    // 带参数构造器，调用父类中带有参数的构造器
    public SubClass(int n) {
        super(300); // 调用父类构造器初始化 n = 300
        System.out.println("SubClass(int n): " + n);
        super.setN(n); // 修改为子类传入的 n
    }
}

class SubClass2 extends SuperClass {

    // 无参数构造器，调用父类中带有参数的构造器
    public SubClass2() {
        super(300);
        System.out.println("SubClass2()");
    }

    // 带参数构造器，自动调用父类的无参数构造器
    public SubClass2(int n) {
        System.out.println("SubClass2(int n): " + n);
        super.setN(n); // 修改为子类传入的 n
    }
}

public class TestSuperSub {
    public static void main(String[] args) {
        System.out.println("------SubClass 类继承------");
        SubClass sc1 = new SubClass();
        SubClass sc2 = new SubClass(100);
        System.out.println("SubClass2.n = " + sc2.getN());

        System.out.println("------SubClass2 类继承------");
        SubClass2 sc3 = new SubClass2();
        SubClass2 sc4 = new SubClass2(200);
        System.out.println("SubClass2.n = " + sc4.getN());
    }
}
```

输出结果为：

```
------SubClass 类继承------
SuperClass()
SubClass()
SuperClass(int n)
SubClass(int n): 100
SubClass2.n = 100
------SubClass2 类继承------
SuperClass(int n)
SubClass2()
SuperClass()
SubClass2(int n): 200
SubClass2.n = 200
```

### 重写

重写（`Override`）是指子类定义了一个与其父类中具有相同名称、参数列表和返回类型的方法，并且子类方法的实现覆盖了父类方法的实现。即外壳不变，核心重写！

重写方法不能抛出新的检查异常或者比被重写方法申明更加宽泛的异常。例如： 父类的一个方法申明了一个检查异常 `IOException`，
但是在重写这个方法的时候不能抛出 `Exception` 异常，因为 `Exception` 是 `IOException` 的父类，抛出 `IOException` 异常或者 `IOException` 的子类异常。

```java
class Animal{
   public void move(){
      System.out.println("动物可以移动");
   }
}
 
class Dog extends Animal{
   public void move(){
      System.out.println("狗可以跑和走");
   }
}
 
public class TestDog{
   public static void main(String args[]){
      Animal a = new Animal(); // Animal 对象
      Animal b = new Dog(); // Dog 对象
 
      a.move();// 执行 Animal 类的方法
 
      b.move();//执行 Dog 类的方法
   }
}
```

上面的例子中，之所以能编译成功，是因为 `Animal` 类中存在 `move` 方法，然而运行时，运行的是特定对象的方法。

```java
class Animal{
   public void move(){
      System.out.println("动物可以移动");
   }
}
 
class Dog extends Animal{
   public void move(){
      System.out.println("狗可以跑和走");
   }
   public void bark(){
      System.out.println("狗可以吠叫");
   }
}
 
public class TestDog{
   public static void main(String args[]){
      Animal a = new Animal(); // Animal 对象
      Animal b = new Dog(); // Dog 对象
 
      a.move();// 执行 Animal 类的方法
      b.move();//执行 Dog 类的方法
      b.bark();
   }
}
```

编译运行结果如下:

```java
TestDog.java:30: cannot find symbol
symbol  : method bark()
location: class Animal
                b.bark();
                 ^
```

该程序将抛出一个编译错误，因为 b 的引用类型 `Animal` 没有 `bark` 方法。

#### Super 关键字

当需要在子类中调用父类的被重写方法时，要使用 super 关键字。

```java
class Animal{
   public void move(){
      System.out.println("动物可以移动");
   }
}
 
class Dog extends Animal{
   public void move(){
      super.move(); // 应用super类的方法
      System.out.println("狗可以跑和走");
   }
}
 
public class TestDog{
   public static void main(String args[]){
 
      Animal b = new Dog(); // Dog 对象
      b.move(); //执行 Dog类的方法
 
   }
}
```
输出结果为：

```
动物可以移动
狗可以跑和走
```

### 重载

重载(overloading) 是在一个类里面，方法名字相同，而参数不同。返回类型可以相同也可以不同。

每个重载的方法（或者构造函数）都必须有一个独一无二的参数类型列表。最常用的地方就是构造器的重载。

重载规则:

* 被重载的方法必须改变参数列表(参数个数或类型不一样);

* 被重载的方法可以改变返回类型；

* 被重载的方法可以改变访问修饰符；

* 被重载的方法可以声明新的或更广的检查异常；

* 方法能够在同一个类中或者在一个子类中被重载；

* 无法以返回值类型作为重载函数的区分标准；

```java
public class Overloading {
    public int test(){
        System.out.println("test1");
        return 1;
    }
 
    public void test(int a){
        System.out.println("test2");
    }   
 
    //以下两个参数类型顺序不同
    public String test(int a,String s){
        System.out.println("test3");
        return "returntest3";
    }   
 
    public String test(String s,int a){
        System.out.println("test4");
        return "returntest4";
    }   
 
    public static void main(String[] args){
        Overloading o = new Overloading();
        System.out.println(o.test());
        o.test(1);
        System.out.println(o.test(1,"test3"));
        System.out.println(o.test("test4",1));
    }
}
```

重写与重载之间的区别

| 区别点     | 重载方法             | 重写方法                                                 |
|-----------|---------------------|----------------------------------------------------------|
| 参数列表   | 必须修改             | 一定不能修改                                             |
| 返回类型   | 可以修改             | 一定不能修改                                             |
| 异常      | 可以修改             | 可以减少或删除，一定不能抛出新的或者更广的异常         |
| 访问      | 可以修改             | 一定不能做更严格的限制（可以降低限制）                 |


### 多态

多态是同一个行为具有多个不同表现形式或形态的能力。

```java
abstract class Animal {  
    abstract void eat();  
}  
  
class Cat extends Animal {  
    public void eat() {  
        System.out.println("吃鱼");  
    }  
    public void work() {  
        System.out.println("抓老鼠");  
    }  
}  
  
class Dog extends Animal {  
    public void eat() {  
        System.out.println("吃骨头");  
    }  
    public void work() {  
        System.out.println("看家");  
    }  
}

public class Test {
    public static void main(String[] args) {  
        Cat a = new Cat();    
        a.eat();              
        a.work();

        Animal b = new Dog();
        b.eat();
        // b.work();  // 这里会报错，因为 Animal 类没有 work() 方法
        Dog c = (Dog) b; 
        c.work();     // 现在可以调用 work() 方法了
    }  
}
```

输出结果为：

```
吃鱼
抓老鼠
吃骨头
看家
```

当使用多态方式调用方法时，首先检查父类中是否有该方法，如果没有，则编译错误；如果有，再去调用子类的同名方法。

### 抽象

在 `Java` 中，抽象类（abstract class） 是一种不能被实例化的类，用于作为其他类的父类，提供通用的字段和方法定义，并要求子类实现某些方法。

```java
abstract class Animal {
    String name;

    // 构造函数
    public Animal(String name) {
        this.name = name;
    }

    // 抽象方法（没有方法体）
    abstract void makeSound();

    // 普通方法
    public void sleep() {
        System.out.println(name + " is sleeping...");
    }
}

class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }

    @Override
    void makeSound() {
        System.out.println(name + " says: Woof!");
    }
}

public class TestAbstract {
    public static void main(String[] args) {
        Animal dog = new Dog("Buddy");
        dog.makeSound();  // Buddy says: Woof!
        dog.sleep();      // Buddy is sleeping...
    }
}
```

### 封装

`Java` 中的 封装（Encapsulation） 是面向对象编程的核心特性之一。它的主要目标是将对象的状态（字段/成员变量）隐藏在内部，
并通过公开的方法（get/set） 来访问或修改这些数据，从而保证数据安全性和一致性。

要点

* 将成员变量设为 private，防止外部直接访问。

* 提供 public 的 getter 和 setter 方法。

* 通过方法控制访问级别与有效性（例如：验证数据合法性）。

```java
public class Person {
    // 私有字段
    private String name;
    private int age;

    // 公有构造器
    public Person(String name, int age) {
        this.name = name;
        setAge(age); // 使用 set 方法，包含合法性校验
    }

    // 公有 Getter
    public String getName() {
        return name;
    }

    // 公有 Setter
    public void setName(String name) {
        this.name = name;
    }

    // 公有 Getter
    public int getAge() {
        return age;
    }

    // 公有 Setter（带校验）
    public void setAge(int age) {
        if (age >= 0 && age <= 150) {
            this.age = age;
        } else {
            System.out.println("年龄不合法！");
        }
    }

    public void introduce() {
        System.out.println("我是 " + name + "，今年 " + age + " 岁。");
    }
}

public class TestPerson {
    public static void main(String[] args) {
        Person p = new Person("张三", 28);
        p.introduce();

        p.setAge(200); // 设置失败，非法数据
        System.out.println("当前年龄：" + p.getAge());
    }
}
```

### 接口

在 `Java` 中，接口（interface） 是一种抽象类型，用于定义类必须实现的一组方法。接口是 `Java` 实现多态和多继承的关键机制


要点

* 接口中的方法默认是 public abstract（即公开的、抽象的）。

* 接口中的变量默认是 public static final（即常量）。

* 类使用 implements 关键字来实现接口。

* 一个类可以实现多个接口，实现接口是支持 多继承 的方式

```java
// 定义接口
interface Animal {
    void speak(); // 接口中的方法默认是 public abstract
    String getType();
}

// 实现接口
class Dog implements Animal {
    @Override
    public void speak() {
        System.out.println("Dog barks.");
    }

    @Override
    public String getType() {
        return "Dog";
    }
}

class Cat implements Animal {
    @Override
    public void speak() {
        System.out.println("Cat meows.");
    }

    @Override
    public String getType() {
        return "Cat";
    }
}

// 测试类
public class TestInterface {
    public static void main(String[] args) {
        Animal a1 = new Dog();
        Animal a2 = new Cat();

        a1.speak(); // Dog barks.
        a2.speak(); // Cat meows.
        System.out.println(a1.getType()); // Dog
    }
}
```

### 枚举

在 `Java` 中，enum（枚举）是一种特殊的类，用于定义常量集合。它是一种类型安全的方式来表示固定集合的值。

```java
enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

public class TestEnum {
    public static void main(String[] args) {
        Day today = Day.MONDAY;
        System.out.println(today); // 输出：MONDAY

        // 使用 switch 语句
        switch (today) {
            case MONDAY:
                System.out.println("Start of the week");
                break;
            case FRIDAY:
                System.out.println("Almost weekend");
                break;
            default:
                System.out.println("Midweek");
        }
    }
}
```

遍历所有枚举值

```java
for (Day day : Day.values()) {
    System.out.println(day);
}  
```
