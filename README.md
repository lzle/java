## 目录

* [基础](#基础)
    * [安装](#安装)



## 基础
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
