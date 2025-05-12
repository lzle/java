## 目录

* [环境](#环境)
    * [安装](#安装)
    * [Hello World](#hello-world)
* [修饰符](#修饰符)
    * [protected](#protected)


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

### protected

在 `Java` 中，`protected` 是一种访问修饰符，用于控制类成员（属性、方法、构造器）的可见性。它的访问范围介于 `private` 和 `public` 之间，具体如下：

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
