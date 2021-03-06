

# J2SE 基础入门，从事 Java 必学！

## J2SE 整体概括

![](https://upload-images.jianshu.io/upload_images/25392987-21477024f3239a7f.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

我们先来了解一下什么是 J2SE。

### J2SE 的定义

J2SE，全称为Java 2 Standard Edition。Java 2 平台包括：标准版（J2SE）、企业版（J2EE）和微缩版（J2ME）三个版本。J2SE 即 Java 2 的标准版，主要用于桌面应用软件的开发。

下面这段话是 ORACLE 对于 Java SE 的官方描述：

> Java Platform, Standard Edition (Java SE) 可以让您在桌面和服务器以及目前要求较高的嵌入式环境中开发和部署 Java 应用程序。 Java 提供了当今应用程序所需要的丰富的用户界面、良好的性能、多功能性、可移植性和安全性。

J2SE 与 J2EE、J2ME 之间的关系可以通过下图来表示：

![img](https:////upload-images.jianshu.io/upload_images/226662-9cafa839962967cd.png!thumbnail?imageMogr2/auto-orient/strip|imageView2/2/w/454/format/webp)

### J2SE 的架构

J2SE 的架构如下图所示，它主要包含了 UI、集成库、语言和工具基础库、其他基础库、Java 虚拟机等组件。

![img](https:////upload-images.jianshu.io/upload_images/226662-6e799f93d2734c91.png!thumbnail?imageMogr2/auto-orient/strip|imageView2/2/w/695/format/webp)

综上所述，将 J2SE 压缩一点再加上一些[CLDC](https://links.jianshu.com/go?to=http%3A%2F%2Fbaike.baidu.com%2Flink%3Furl%3DYyhiiGfjgAR-CzCLq5nHUKwDvAKRCTC-JDmf_uAcYyqJerKQaB36sLlFNzoO9JtrutrOH1UnbAZjs7lrcmJKRK)等方面的特性就是 J2ME；将其扩充一点再增加一些 EJB 等企业应用方面的特性就是 J2EE。因此 J2SE 是 J2EE 的基础，建议从事 Java 的开发人员从 J2SE 开始学习。

## 面对对象

在前面 Java 基础语法的学习中，你应该接触了一些面向对象的基础知识。面向对象的概念在 Java 的开发体系中无处不在，在今后的开发过程中，你也应该以面向对象的思想来看待和解决问题。

既然是面向对象，就会谈论到类和对象的概念，以及它们之间的关系：

> 类是现实世界或思维世界中的实体在计算机中的反映，它将数据以及这些数据上的操作封装在一起。对象是具有类类型的变量。
>
> 类是对象的抽象，而对象是类的具体实例。类是抽象的，不占用内存，而对象是具体的，占用存储空间。类是用于创建对象的蓝图，它是一个定义包括在特定类型的对象中的方法和变量的软件模板。

下面，我们通过一些例子来巩固面向对象的相关知识。



## 图书管理系统实验

### 自定义图书类

我们首先在 Eclipse 中创建一个名为`HelloJ2SE`的 Java Project，这里我们选用 Java 1.8，再在 src 文件夹下新建一个名为`com.shiyanlou.course`的包。

![img](https:////upload-images.jianshu.io/upload_images/226662-0f0b22ad07ee75ec.png!thumbnail?imageMogr2/auto-orient/strip|imageView2/2/w/920/format/webp)

注意：我们建议你在之后的项目创建中都使用 1.8 版本

然后我们在这个包里添加一个`Book`类。

![img](https:////upload-images.jianshu.io/upload_images/226662-c30a7ecbf0709ea5.png!thumbnail?imageMogr2/auto-orient/strip|imageView2/2/w/786/format/webp)

对于一个图书类，一般有书名、作者和编码等属性。我们利用这些常见属性来自定义这个图书类，创建的`Book.java`文件中主要代码如下：

特别说明： 在实验楼的实验环境中，暂不支持输入中文，因此你不必将代码片段中的注释也输入开发环境。该说明同样适用于本课程后续的章节。



```tsx
package com.shiyanlou.course;
//此为包名，如果你在创建包时已自动生成了该行，请忽略

public class Book {
    private String name; // 书名
    private String author; // 作者
    private String ISBN; // 编码
    //Tips: ISBN是国际标准书号，每本书背面的条形码即为此物

    public Book(String name, String author, String ISBN) {
    // 利用构造方法初始化域
        this.name = name;
        this.author = author;
        this.ISBN = ISBN;

        //Q:你清楚this的用法吗？
    }

    public String getName() { // 获得书名
        return name;
    }
    public String getAuthor() { // 获得作者
        return author;
    }
    public String getISBN() { // 获得编码
        return ISBN;
    }
}
```

为了测试我们刚刚自定义的图书类，我们在com.shiyanlou.course这个包中再创建一个名为`Test`的类文件，并在`main()`方法中创建一个Book对象。最后，我们在控制台输出这个Book对象的属性。

创建的Test.java文件中，主要的代码如下：



```csharp
package com.shiyanlou.course;

public class Test {
    public static void main(String[] args) {
        Book book = new Book("This is my 1st book", "Peter", "1234567890");
        // 创建Book对象并设定其各个属性
        System.out.println("Book Name: " + book.getName());
        // 输出这本书的名字
        System.out.println("Book Author: " + book.getAuthor());
        // 输出这本书的作者
        System.out.println("ISBN: " + book.getISBN());
        // 输出这本书的编码
    }
}
```

点击编译并运行。

![img](https:////upload-images.jianshu.io/upload_images/226662-1d7348c8253abd74.png!thumbnail?imageMogr2/auto-orient/strip|imageView2/2/w/167/format/webp)

如果在控制台中可以看到下图这样的信息，那么祝贺你，一个自定义的图书类就成功完成了。

![img](https:////upload-images.jianshu.io/upload_images/226662-4d7fc9689ecbc43a.png!thumbnail?imageMogr2/auto-orient/strip|imageView2/2/w/485/format/webp)

当然，你也可以为`Book`类添加更多的属性，并为每个属性编写`get`方法。

### 动态化实例类

在面向对象的编程中，把用类创建对象的过程称为实例化。通常是使用有参数或无参数的构造方法来创建对象。其格式如下：



```cpp
//有参数的情形
CLASS_NAME OBJECT_NAME = new CLASS_NAME(parameter_1,...parameter_n);

//例如下面这个例子
Person peter = new Person("Peter","boy");

//无参数的情形
CLASS_NAME OBJECT_NAME = new CLASS_NAME();

//例如下面这个例子
Dog dog_1 = new Dog();
```

你可以仿照自定义图书类的例子，通过自己创建相关的`Person`类和`Dog`类以及测试的方法来验证上述过程。

但是在 Java 中，类的实例化方法一共有四种途径：

1. 使用new操作符
2. 调用 Class 对象的newInstance()方法
3. 调用clone()方法，对现有实例的拷贝
4. 通过ObjectInputStream的readObject()方法反序列化类

我们在自定义图书类这个例子中，编写了有参数的构造方法public Book(String name, String author, String ISBN)。但如果类中没有定义构造方法，编译器便会自动添加一个无参数的构造方法。使用构造方法创建对象虽然常用，但并不灵活。因此，我们再来了解一下动态化实例类，也就是调用 Class 对象的newInstance()方法，通过反射创建对象。

了解一下反射的概念：

> JAVA 反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性；这种动态获取信息以及动态调用对象的方法的功能称为 java 语言的反射机制。

那么我们就开始来学习如何动态化实例类：

请在 Eclipse 中创建一个项目DynamicClass，并在该项目中创建com.shiyanlou.course包。在该包中创建Test类，并编写main()方法。

在main()方法中创建一个 File 对象（你只需要知道 File 对象也是一个对象即可，[进一步了解 File 对象](https://links.jianshu.com/go?to=http%3A%2F%2Fdocs.oracle.com%2Fjavase%2F7%2Fdocs%2Fapi%2Fjava%2Fio%2FFile.html)）。

最后，使用该对象在桌面创建一个文本文件。

主要的代码如下：



```kotlin
package com.shiyanlou.course;

import java.io.File;
import java.lang.reflect.Constructor;
//需要引用上述两个包

public class Test {

        public static void main(String[] args) {
            try {

                Constructor<File> constructor = File.class.getDeclaredConstructor(String.class);
                //获得File类的Constructor对象

                System.out.println("Create File Object with reflection.");
                //使用反射创建File对象
                File file = constructor.newInstance("/home/shiyanlou/Desktop/MyFile.txt");
                System.out.println("Use File Object to create MyFile.txt on desktop.");
                //指定了创建的路径为桌面，名称为“MyFile.txt”

                file.createNewFile(); //创建新的文件
                System.out.println("File is created ?" + file.exists());
                //验证文件是否创建成功

            } catch (Exception e) {
                e.printStackTrace();
            }
       }
}
```

你可能会问为什么会用到`try`、`catch`以及`Exception`之类的奇怪的东西，这是由于上述代码会抛出大量的异常。我们通常不推荐这样写。不用担心，我们将在错误处理一章为你详细介绍他们的原理和用法。

点击编译并运行，如果在控制台可以看到下列信息则表示你成功了。

![img](https:////upload-images.jianshu.io/upload_images/226662-6618226b5b038b1a.png!thumbnail?imageMogr2/auto-orient/strip|imageView2/2/w/539/format/webp)

同时，你也应该可以在桌面上发现自己创建的这个`MyFile.txt`文件。

![img](https:////upload-images.jianshu.io/upload_images/226662-ff77aaa789cb7c6e.png!thumbnail?imageMogr2/auto-orient/strip|imageView2/2/w/211/format/webp)



