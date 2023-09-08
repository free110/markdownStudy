# Java语法

> 1. 在java原文件当中最多只能有一个public类，并且该类的名称要与**源文件**一致。

## 注释

![image-20230808143251485](image/image-20230808143251485.png)

- **具体使用：文档注释（Java特有）**

  - 文档注释内容可以被JDK提供的工具 javadoc 所解析，生成一套以网页文件形式体现的该程序的说明文档。

  - 操作方式。比如：

    ```
    javadoc -d mydoc -author -version HelloWorld.java
    ```

## 命名规范

![image-20230808183219278](image/image-20230808183219278.png)

**注意** ：long类型声明赋值的时候一定末尾带有L，对于float类型要带有f。开发过程中会发现float类型精度不高，这个时候要使用BigDecimal类来进行计算  

在**char**类型中可以将数字与符号互通，就像c语言的ascll值一样，但是注意需要用`\u`*(unicode编码格式)*来进行转义，当然也可以使用转移符号`\`

**注意** 逻辑&和短路&&表示的含义不一样

```
语句1&语句2 #当语句1为false时，语句2也会执行；
语句1&&语句2 #当语句1为false时，语句2不会执行；

```

# 面向对象编程

![image-20230814223901062](image/image-20230814223901062.png)

## 成员变量与局部变量

![image-20230814230626847](image/image-20230814230626847.png)

![image-20230814230644698](image/image-20230814230644698.png)

### 成员变量与局部变量的不同

![image-20230814230727473](image/image-20230814230727473.png)

**类中存在属性（变量，全局变量）和方法**；很容易根据以前学习过的内容理解

> 除了固定的重载方法之外，和python一样还有可变个数形参的方法定义
>
> 例如： public void test(int ... nums){}
>
> 这个方法就定义了可变个数的方法 ，但是这种定义与下面的方法定义是相同的
>
> public void test(int[] nums){}
>
> **两种方法都是直接将nums看作数组**
>
> 注意：当定义 public void test(int i, int ... nums){}
>
> **这里要求nums必须放在最后，而且nums在一个函数定义中只能出现一次**

 ## 封装性

主要使用四种修饰符：**private、protected、public、缺省**

![image-20230816161955109](image/image-20230816161955109.png)

**注意** 类只有public和缺省修饰，类内的成员才可以使用四种修饰符

### 构造器

> 定义构造器的格式：
>
> ``` 权限修饰符 类名(形参列表){}```
>
> 定义有参构造器之后，系统的空参构造器将会无效
>
> **可以使用this(形参列表)表示构造器调用，并且要放在首行**
>
> 

## 继承性

**关键字**extends

1. 子类 虽然继承了父类的属性和方法，但是并没有打破封装性。

2. 单继承性，可以多层继承

   ### 方法重写

   1. 父类被重写的方法与子类重写的方法的方法名和形参列表要相同

   2. 子类重写的方法 权限修饰符要不小于父类被重写的方法权限修饰符；**子类无法重写父类中private的方法**

      针对返回值有要求 ：

      > 1. 父类的方法返回值是void，那么子类方法应该保持void
      > 2. 父类的返回值是基本数据类型，子类也必须保持与父类相同
      > 3. 父类的返回值是引用数据类型（比如：类），子类方法返回值可以保持相同或者是子类。

      针对与子类重写方法抛出异常的规定：

      > 子类重写方法抛出的异常应该是父类被重写方法抛出异常的子类或者相同

      ### 关于super与this

      ![image-20230818235430678](image/image-20230818235430678.png)

## 多态

多态性适用于方法，不适用于属性

person pr = new man();

pr.eat（）；

假如person有eat方法，在man类中有eat和sleep方法，在编译时pr是person类型，执行时当作man类型；但是无法调用sleep方法，可以调用eat（）方法，因为这个方法是重写的。多态性调用方法时，只能调用父类和子类共有的方法。但是在内存中是存在着sleep方法的。

**向下转型：**

> 使用关键词**instanceof**

**object类**

> 这个类是所有类的根类
>
> 我们重点掌握这个类的内部方法
>
> 1. **重点方法**：equals、toString
> 2. clone（）、finalize
> 3. 目前不需要关注：grtClass（）/hashCode()/ notify()/ notifyAll()/ wait()/ wait(x)/ wait(x,y)

**equals（）方法**

> 只能使用在引用数据类型；**还要了解equals的内部源码，尤其是他们的写法**
>
>  

**toString方法**

> 原始的方法是返回地址，后面需要根据自己的需求在新的类中重写，这个方法会在输出时自动调用

**static**

> static修饰的变量在内存中只会存在一份，但是可以修改
>
> ![image-20230821215424647](image/image-20230821215424647.png)
>
> **静态方法内可以使用静态属性和静态方法，但是无法调用实例方法和属性**

## 单例模式

> 1. 饿汉式：线程上安全，但是会有内存的占用增多 
> 2. 懒汉式：线程上是不安全的

## 代码块

> 格式 
>
> ```
> class Person{
> 	static{
> 		//静态代码块
> 	}
> 	{
> 		//非静态代码块
> 	}
> }
> ```
>
> 1. 静态代码块随着类的加载而执行，由于类的加载只有一次，所以静态代码块只会执行一次
>
> 2. 非静态代码块随着对象的创建而执行；对象可以有多个，所以非静态代码块可以执行很多次
>
>    **代码块的执行是早于构造器的，牢记加载时父类先加载，子类后加载**



## 关键字final

> 修饰类表明该类无法被继承，修饰方法表明该方法无法被重写 ；可以修饰成员变量和局部变量，表明无法更改变量的值
>
> final修饰成员变量，变量必须要通过显式赋值、代码块赋值、构造器赋值，三种方式中的一种然后变量就无法更改了。
>
> final修饰局部变量，必须在调用前进行赋值，赋值后就无法进行更改。





## abstract

> 1. 可以修饰类，方法。
>
> 2. 修饰方法时，该类必须为抽象类
>
> 3. 修饰方法时，格式：
>
>    ```
>    权限修饰符 abstract 返回值类型 方法名（）；//不允许有大括号和方法体，子类应该重写该方法
>    ```
>
>     
>
> 4. 子类必须重写父类中所有的抽象方法才可以实例化，否则仍是抽象类
>
> 5. abstract不能修饰私有方法、静态方法、final类、final方法

## interface接口

定义接口格式：

```
interface 名字{
	属性
	方法
}
```

类实现接口：关键词为implements

```
权限修饰符 class 类名 extends 父类  implements 接口名1，接口名2{
	//实现接口中的方法，如果不想实现，权限修饰符要为abstract(即抽象类)
}
```

1. 可以声明

   > 属性：只能使用public static final 修饰
   >
   > 方法：jdk8之前：声明抽象方法，public abstract 修饰；**jdk8可以声明静态方法、默认方法；jdk9可以声明私有方法，这些方法中允许放方法体了**
   >
   > **注意**：1. 接口中声明的静态方法只能通过接口调用，无法通过其实现类进行调用
   >
   > 			2. 默认方法关键词：default
   > 			2. 默认方法是可以通过实现类的对象进行调用的，当然实现类也可以对默认方法进行重写
   > 			2. 类实现了两个接口，两个接口都有同名同参数的默认方法，如果实现类还没有重写该方法，就会出现接口冲突，在这种情况下，实现类应该重写该默认方法
   > 			2. 子类继承了父类并且实现接口，接口和父类有同名同参数方法，子类还没有重写的情况下，父类的方法优先于接口 
   > 			2. 如果子类想要调用实现接口中的方法，比如eat方法，这个方法在接口A中有，在子类中也有，但是希望在子类中调用A中的，可以用A.super.eat();进行调用。
   > 			2. 接口中私有方法就是为了给默认方法提供的，把重复代码提炼出来放到私有方法中

2. 不可以声明

   > 构造器、代码块

3. 接口本身和类一样可以实现继承，并且可以实现多继承

   ```
   interface cc extends aa,bb{
   
   }
   ```

4. 接口本身可以实现多态，类似于类

   ```java
   interface USB{
   	void print();
   }
   class camer implements USB{
   	void print(){
   	
   	}
   }
   
   class computer{
   	void pr(USB usb){
   	
   	}
   }
   
   
   main{
   	computer co = new computer();
   	camer ca = new camer();
   	co.pr(ca);
   }
   //这就是接口的多态性，类似于类的多态性 
   格式为：接口名 变量名 = new 实现类对象；
   
   //还有一种写法，这里传入pr的参数为一个没有名字的类，该类实现了接口USB
   main{
   	computer co = new computer();
   	
   	co.pr(new USB{
           void print{
               方法体
           }
       });
   }
   
   
   ```

   

## 内部类

分类：

1. 成员内部类：直接声明在外部类的里面

    1. 静态成员内部类，用static修饰，和外部了相关联

    2. 非静态成员内部类，不使用static修饰，和对象相关联

       ![image-20230824135207085](image/image-20230824135207085.png)

       

2. 局部内部类：声明在方法、构造器、代码块里面

   	1. 匿名局部内部类
   	1. 非匿名局部内部类

## 枚举类

针对于某个类，其实例对象个数是确定的，就可以考虑从枚举类

关键词：enum，自动继承父类Enum；枚举类本身可以实现接口

### 1.enum关键字声明枚举

```java
【修饰符】 enum 枚举类名{
    常量对象列表
}

【修饰符】 enum 枚举类名{
    常量对象列表;
    
    对象的实例变量列表;
}
```

举例1：

```java
package com.atguigu.enumeration;

public enum Week {
    MONDAY,TUESDAY,WEDNESDAY,THURSDAY,FRIDAY,SATURDAY,SUNDAY;
}
```

```java
public class TestEnum {
	public static void main(String[] args) {
		Season spring = Season.SPRING;
		System.out.println(spring);
	}
}
```

举例2：

```java
public enum SeasonEnum {
    SPRING("春天","春风又绿江南岸"),
    SUMMER("夏天","映日荷花别样红"),
    AUTUMN("秋天","秋水共长天一色"),
    WINTER("冬天","窗含西岭千秋雪");

    private final String seasonName;
    private final String seasonDesc;
    
    private SeasonEnum(String seasonName, String seasonDesc) {
        this.seasonName = seasonName;
        this.seasonDesc = seasonDesc;
    }
    public String getSeasonName() {
        return seasonName;
    }
    public String getSeasonDesc() {
        return seasonDesc;
    }
}

```

###  2. enum中常用方法

```
String toString(): 默认返回的是常量名（对象名），可以继续手动重写该方法！
    
static 枚举类型[] values():返回枚举类型的对象数组。该方法可以很方便地遍历所有的枚举值，是一个静态方法
    
static 枚举类型 valueOf(String name)：可以把一个字符串转为对应的枚举类对象。要求字符串必须是枚举类对象的“名字”。如不是，会有运行时异常：IllegalArgumentException。
    
String name():得到当前枚举常量的名称。建议优先使用toString()。
    
int ordinal():返回当前枚举常量的次序号，默认从0开始
```

## annotation(注解)

使用的关键词： @interface

**元注解：对现有的注解进行解释说明的注解**

![image-20230824221806276](image/image-20230824221806276.png)

![image-20230824221941188](image/image-20230824221941188.png)

## 单元测试

### 1. 引入本地JUnit.jar

第1步：在项目中File-Project Structure中操作：添加Libraries库

<img src="image/image-20211228180938922.png" alt="image-20211228180938922" style="zoom:80%;" />

![image-20221002195547325](image/image-20221002195547325.png)

其中，junit-libs包内容如下：

![image-20220813005206452](image/image-20220813005206452.png)

第2步：选择要在哪些module中应用JUnit库

![image-20220813005511062](image/image-20220813005511062.png)

第3步：检查是否应用成功

![image-20220813005729233](image/image-20220813005729233.png)

**注意Scope：选择Compile，否则编译时，无法使用JUnit。**

第4步：下次如果有新的模块要使用该libs库，这样操作即可

![image-20220813005944022](image/image-20220813005944022.png)

![image-20220813010018152](image/image-20220813010018152.png)

![image-20220813010055217](image/image-20220813010055217.png)

![image-20220813010124381](image/image-20220813010124381.png)

### 2. 条件

![image-20230824224210683](image/image-20230824224210683.png)

## 包装类

![image-20230825230040312](C:\Users\1953287730\AppData\Roaming\Typora\typora-user-images\image-20230825230040312.png)

  **注意：基本数据类型转包装类，调用方法valuOf（）；包装类转基本数据类型，调用方法XXXvalue（）**

但是我们一般转换不会用上面的方法，jdk5以后有了新特性：自动装箱、自动拆箱

```
自动装箱
int k =10;
Integer in = k;//这就是自动装箱

//自动拆箱
int m = in;//这就是自动拆箱
```

## String与基本数据类型转换

、![image-20230826000614318](C:\Users\1953287730\AppData\Roaming\Typora\typora-user-images\image-20230826000614318.png)

前面的部分忘记知识点补充：三目运算符中会有自动类型提升



# IntelliJ IDEA 常用快捷键一览表

author：尚硅谷-宋红康

***

## 1-IDEA的日常快捷键

### 第1组：通用型

| 说明            | 快捷键           |
| --------------- | ---------------- |
| 复制代码-copy   | ctrl + c         |
| 粘贴-paste      | ctrl + v         |
| 剪切-cut        | ctrl + x         |
| 撤销-undo       | ctrl + z         |
| 反撤销-redo     | ctrl + shift + z |
| 保存-save all   | ctrl + s         |
| 全选-select all | ctrl + a         |

### 第2组：提高编写速度（上）

| 说明                                               | 快捷键           |
| -------------------------------------------------- | ---------------- |
| 智能提示-edit                                      | alt + enter      |
| 提示代码模板-insert live template                  | ctrl+j           |
| 使用xx块环绕-surround with ...                     | ctrl+alt+t       |
| 调出生成getter/setter/构造器等结构-generate ...    | alt+insert       |
| 自动生成返回值变量-introduce variable ...          | ctrl+alt+v       |
| 复制指定行的代码-duplicate line or selection       | ctrl+d           |
| 删除指定行的代码-delete line                       | ctrl+y           |
| 切换到下一行代码空位-start new line                | shift + enter    |
| 切换到上一行代码空位-start new line before current | ctrl +alt+ enter |
| 向上移动代码-move statement up                     | ctrl+shift+↑     |
| 向下移动代码-move statement down                   | ctrl+shift+↓     |
| 向上移动一行-move line up                          | alt+shift+↑      |
| 向下移动一行-move line down                        | alt+shift+↓      |
| 方法的形参列表提醒-parameter info                  | ctrl+p           |

### 第3组：提高编写速度（下）

| 说明                                        | 快捷键       |
| ------------------------------------------- | ------------ |
| 批量修改指定的变量名、方法名、类名等-rename | shift+f6     |
| 抽取代码重构方法-extract method ...         | ctrl+alt+m   |
| 重写父类的方法-override methods ...         | ctrl+o       |
| 实现接口的方法-implements methods ...       | ctrl+i       |
| 选中的结构的大小写的切换-toggle case        | ctrl+shift+u |
| 批量导包-optimize imports                   | ctrl+alt+o   |

### 第4组：类结构、查找和查看源码

| 说明                                                      | 快捷键                          |
| --------------------------------------------------------- | ------------------------------- |
| 如何查看源码-go to class...                               | ctrl + 选中指定的结构 或 ctrl+n |
| 显示当前类结构，支持搜索指定的方法、属性等-file structure | ctrl+f12                        |
| 退回到前一个编辑的页面-back                               | ctrl+alt+←                      |
| 进入到下一个编辑的页面-forward                            | ctrl+alt+→                      |
| 打开的类文件之间切换-select previous/next tab             | alt+←/→                         |
| 光标选中指定的类，查看继承树结构-Type Hierarchy           | ctrl+h                          |
| 查看方法文档-quick documentation                          | ctrl+q                          |
| 类的UML关系图-show uml popup                              | ctrl+alt+u                      |
| 定位某行-go to line/column                                | ctrl+g                          |
| 回溯变量或方法的来源-go to implementation(s)              | ctrl+alt+b                      |
| 折叠方法实现-collapse all                                 | ctrl+shift+ -                   |
| 展开方法实现-expand all                                   | ctrl+shift+ +                   |

### 第5组：查找、替换与关闭

| 说明                                               | 快捷键       |
| -------------------------------------------------- | ------------ |
| 查找指定的结构                                     | ctlr+f       |
| 快速查找：选中的Word快速定位到下一个-find next     | ctrl+l       |
| 查找与替换-replace                                 | ctrl+r       |
| 直接定位到当前行的首位-move caret to line start    | home         |
| 直接定位到当前行的末位 -move caret to line end     | end          |
| 查询当前元素在当前文件中的引用，然后按 F3 可以选择 | ctrl+f7      |
| 全项目搜索文本-find in path ...                    | ctrl+shift+f |
| 关闭当前窗口-close                                 | ctrl+f4      |

### 第6组：调整格式

| 说明                                         | 快捷键           |
| -------------------------------------------- | ---------------- |
| 格式化代码-reformat code                     | ctrl+alt+l       |
| 使用单行注释-comment with line comment       | ctrl + /         |
| 使用/取消多行注释-comment with block comment | ctrl + shift + / |
| 选中数行，整体往后移动-tab                   | tab              |
| 选中数行，整体往前移动-prev tab              | shift + tab      |

## 2-Debug快捷键

| 说明                                                  | 快捷键        |
| ----------------------------------------------------- | ------------- |
| 单步调试（不进入函数内部）- step over                 | F8            |
| 单步调试（进入函数内部）- step into                   | F7            |
| 强制单步调试（进入函数内部） - force step into        | alt+shift+f7  |
| 选择要进入的函数 - smart step into                    | shift + F7    |
| 跳出函数 - step out                                   | shift + F8    |
| 运行到断点 - run to cursor                            | alt + F9      |
| 继续执行，进入下一个断点或执行完程序 - resume program | F9            |
| 停止 - stop                                           | Ctrl+F2       |
| 查看断点 - view breakpoints                           | Ctrl+Shift+F8 |
| 关闭 - close                                          | Ctrl+F4       |

# 异常处理

**注意：异常（Exception）属于代码错误或者未知问题，可以通过处理进行解决；如果是错误（Error），这个不属于异常的范围，无法进行处理**

异常分为编译时异常和运行时异常：

下面是1-2年经常出现的异常：

![image-20230826182423783](C:\Users\1953287730\AppData\Roaming\Typora\typora-user-images\image-20230826182423783.png)





在catch捕捉异常的时候，如果异常同时存在子类和父类，那么父类应该在子类的下面

![image-20230826210631930](C:\Users\1953287730\AppData\Roaming\Typora\typora-user-images\image-20230826210631930.png)

finally中的东西是被强制执行的，一般一些资源的关闭会写在这里面。

**通过throws抛出异常，这个是抛给了方法调用者，仍就需要调用者提供解决方案；通过throw手动抛出异常，这个是在方法体中写的，格式为 throw new 异常类对象(信息)；抛出异常不要写到main中，会挂掉虚拟机**

![image-20230828225014522](C:\Users\1953287730\AppData\Roaming\Typora\typora-user-images\image-20230828225014522.png)

# 多线程

## 2.创建和启动线程

### 2.1 概述

- Java语言的JVM允许程序运行多个线程，使用`java.lang.Thread`类代表**线程**，所有的线程对象都必须是Thread类或其子类的实例。

- Thread类的特性
  - 每个线程都是通过某个特定Thread对象的run()方法来完成操作的，因此把run()方法体称为`线程执行体`。
  - 通过该Thread对象的start()方法来启动这个线程，而非直接调用run()
  - 要想实现多线程，必须在主线程中创建新的线程对象。

### 2.2 方式1：继承Thread类

Java通过继承Thread类来**创建**并**启动多线程**的步骤如下：

1. 定义Thread类的子类，并重写该类的run()方法，该run()方法的方法体就代表了线程需要完成的任务
2. 创建Thread子类的实例，即创建了线程对象
3. 调用线程对象的start()方法来启动该线程

代码如下：

~~~java
package com.atguigu.thread;
//自定义线程类
public class MyThread extends Thread {
    //定义指定线程名称的构造方法
    public MyThread(String name) {
        //调用父类的String参数的构造方法，指定线程的名称
        super(name);
    }
    /**
     * 重写run方法，完成该线程执行的逻辑
     */
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(getName()+"：正在执行！"+i);
        }
    }
}
~~~

测试类：

~~~java
package com.atguigu.thread;

public class TestMyThread {
    public static void main(String[] args) {
        //创建自定义线程对象1
        MyThread mt1 = new MyThread("子线程1");
        //开启子线程1
        mt1.start();
        
        //创建自定义线程对象2
        MyThread mt2 = new MyThread("子线程2");
        //开启子线程2
        mt2.start();
        
        //在主方法中执行for循环
        for (int i = 0; i < 10; i++) {
            System.out.println("main线程！"+i);
        }
    }
}

~~~

<img src="D:\桌面\尚硅谷Java基础\01_课件与电子教材\01_课件与电子教材\01_课件与电子教材\尚硅谷_第10章_多线程\images\image-20220401221215860.png" alt="image-20220401221215860" style="zoom:67%;" />

> 注意：
>
> 1. 如果自己手动调用run()方法，那么就只是普通方法，没有启动多线程模式。
>
> 2. run()方法由JVM调用，什么时候调用，执行的过程控制都有操作系统的CPU调度决定。
>
> 3. 想要启动多线程，必须调用start方法。
>
> 4. 一个线程对象只能调用一次start()方法启动，如果重复调用了，则将抛出以上的异常“`IllegalThreadStateException`”。

### 2.3 方式2：实现Runnable接口

Java有单继承的限制，当我们无法继承Thread类时，那么该如何做呢？在核心类库中提供了Runnable接口，我们可以实现Runnable接口，重写run()方法，然后再通过Thread类的对象代理启动和执行我们的线程体run()方法

步骤如下：

1. 定义Runnable接口的实现类，并重写该接口的run()方法，该run()方法的方法体同样是该线程的线程执行体。
2. 创建Runnable实现类的实例，并以此实例作为Thread的target参数来创建Thread对象，该Thread对象才是真正
   的线程对象。

3. 调用线程对象的start()方法，启动线程。调用Runnable接口实现类的run方法。

代码如下：

```java
package com.atguigu.thread;

public class MyRunnable implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            System.out.println(Thread.currentThread().getName() + " " + i);
        }
    }
}
```

测试类：

```java
package com.atguigu.thread;

public class TestMyRunnable {
    public static void main(String[] args) {
        //创建自定义类对象  线程任务对象
        MyRunnable mr = new MyRunnable();
        //创建线程对象
        Thread t = new Thread(mr, "长江");
        t.start();
        for (int i = 0; i < 20; i++) {
            System.out.println("黄河 " + i);
        }
    }
}
```

 通过实现Runnable接口，使得该类有了多线程类的特征。所有的分线程要执行的代码都在run方法里面。

在启动的多线程的时候，需要先通过Thread类的构造方法Thread(Runnable target) 构造出对象，然后调用Thread对象的start()方法来运行多线程代码。

实际上，所有的多线程代码都是通过运行Thread的start()方法来运行的。因此，不管是继承Thread类还是实现
Runnable接口来实现多线程，最终还是通过Thread的对象的API来控制线程的，熟悉Thread类的API是进行多线程编程的基础。

说明：Runnable对象仅仅作为Thread对象的target，Runnable实现类里包含的run()方法仅作为线程执行体。
而实际的线程对象依然是Thread实例，只是该Thread线程负责执行其target的run()方法。

<img src="D:\桌面\尚硅谷Java基础\01_课件与电子教材\01_课件与电子教材\01_课件与电子教材\尚硅谷_第10章_多线程\images\image-20220401222212377.png" alt="image-20220401222212377"  />

