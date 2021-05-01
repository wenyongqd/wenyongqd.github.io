---
title: 恕我直言你可能真的不会Java
subtitle: “Make the choices today that pay you back tomorrow.”
date: 2020-04-25 10:48:33
tags:
---

<!-- TOC -->

- [1. Lambda 表达式会用了吗？](#1-lambda-表达式会用了吗)
  - [一、接口定义](#一接口定义)
  - [二、传统的接口函数实现方式](#二传统的接口函数实现方式)
  - [三、lambda 表示式实现方式](#三lambda-表示式实现方式)
- [2. 初识 Stream-API](#2-初识-stream-api)
  - [一、什么是 Java Stream API？](#一什么是-java-stream-api)
  - [二、Stream API 代替 for 循环](#二stream-api-代替-for-循环)
  - [三、将数组转换为管道流](#三将数组转换为管道流)
  - [四、将集合类对象转换为管道流](#四将集合类对象转换为管道流)
  - [五、将文本文件转换为管道流](#五将文本文件转换为管道流)
- [3. Stream 的 filter 与谓语逻辑](#3-stream-的-filter-与谓语逻辑)
  - [一、基础代码准备](#一基础代码准备)
  - [二、什么是谓词逻辑？](#二什么是谓词逻辑)
  - [三、谓词逻辑的复用](#三谓词逻辑的复用)
    - [and 语法（并集）](#and-语法并集)
    - [or 语法（交集）](#or-语法交集)
    - [negate 语法（取反）](#negate-语法取反)
- [4. Stream 管道流的 map 操作](#4-stream-管道流的-map-操作)
  - [一、回顾 Stream 管道流 map 的基础用法](#一回顾-stream-管道流-map-的基础用法)
  - [二、处理非字符串类型集合元素](#二处理非字符串类型集合元素)
  - [三、再复杂一点：处理对象数据格式转换](#三再复杂一点处理对象数据格式转换)
  - [四、flatMap](#四flatmap)
- [5.Stream 的状态与并行操作](#5stream-的状态与并行操作)
  - [一、回顾 Stream 管道流操作](#一回顾-stream-管道流操作)
  - [二、中间操作：有状态与无状态](#二中间操作有状态与无状态)
  - [三、Limit 与 Skip 管道数据截取](#三limit-与-skip-管道数据截取)
  - [四、Distinct 元素去重](#四distinct-元素去重)
  - [五、Sorted 排序](#五sorted-排序)
  - [六、串行、并行与顺序](#六串行并行与顺序)

<!-- /TOC -->

## 1. Lambda 表达式会用了吗？

### 一、接口定义

lambda 表达式表达接口函数的实现，在传统的开发方式下，我们不习惯将代码块传递给函数。我们所有的行为定义代码都封装在方法体内，并通过对象引用执行，就像使用下面的代码一样：

```java
public class LambdaDemo {
    //函数定义
    public void printSomething(String something) {
        System.out.println(something);
    }
    //通过创建对象调用函数
    public static void main(String[] args) {
        LambdaDemo demo = new LambdaDemo();
        String something = "I am learning Lambda";
        demo.printSomething(something);
    }
}
```

大家应该对上面的代码的开发方式不感到陌生，这是经典 OOP 的实现样式。下面我们对上面的代码做一个修改，创建一个功能接口，并对该接口定义抽象方法。

```java
public class LambdaDemo {
    //抽象功能接口
    interface Printer {
        void print(String val);
    }
    //通过参数传递功能接口
    public void printSomething(String something, Printer printer) {
        printer.print(something);
    }
}
```

### 二、传统的接口函数实现方式

在上述实现中，Printer 接口负责打印行为，可以是控制台打印，也可以是其他的打印行为。方法 printSomething 不再定义行为，而是执行 Printer 定义的行为，这样的设计更加灵活。代码如下：

```java
public static void main(String[] args) {
    LambdaDemo demo = new LambdaDemo();
    String something = "I am using a Functional interface";
    //实现Printer接口
    Printer printer = new Printer() {
        @Override
        public void print(String val) {
            //控制台打印
            System.out.println(val);
        }
    };
    demo.printSomething(something, printer);
}
```

至此我们都尚未使用 lambda 表达式。我们仅创建了 Printer 接口的具体实现，并将其传递给 printSomething 方法。

### 三、lambda 表示式实现方式

我们先来学习一下 lambda 表达式的语法：

```java
（param1，param2，param3 ...，paramN）-  > {   //代码块；  }
```

- 首先我们知道 lambda 表达式，表达的是接口函数
- 箭头左侧是函数的逗号分隔的形式参数列表
- 箭头右侧是函数体代码

现在，我们使用 lambda 表达式重构一下第一小节中的代码

```java
public static void main(String[] args) {
    LambdaDemo demo = new LambdaDemo();
    String something = "I am learning Lambda";
    //实现Printer接口（请关注下面这行lambda表达式代码）
    Printer printer = (String toPrint)->{System.out.println(toPrint);};
    //调用接口打印
    demo.printSomething(something, printer);
}
```

lambda 表达式使我们代码更简洁。对比传统 java 代码的实现方式，代码量是不是减少了很多？但这仍然不是最简的实现方式，我们一步一步来。

```java
Printer printer = (String toPrint)->{System.out.println(toPrint);};
//简化：去掉参数类型
Printer printer = (toPrint)->{System.out.println(toPrint);};
//简化：去掉参数括号
Printer printer = toPrint->{System.out.println(toPrint);};
//简化：去掉函数体花括号
Printer printer = toPrint->System.out.println(toPrint);
```

- 即使没有在箭头的左侧指定参数的类型，编译器也会从接口方法的形式参数中推断出其类型
- 当只有一个参数的时候，我们完全可以省略参数的括号
- 当函数体只有一行的时候，我们完全可以省略函数体花括号

如果我们的接口方法定义不带任何参数，则可以用空括号替换：

```java
（）->  System.out.println("anything you wan to print")
```

那么，我们最终通过 lambda 表达式，简化完成的代码是什么样的呢？庐山真面目：

```java
public static void main(String[] args) {
    LambdaDemo demo = new LambdaDemo();
    String something="I am Lambda";
    //关注下面的这行代码
    demo.printSomething(something, toPrint -> System.out.println(toPrint));
}
```

lambda 表达式表达的是接口函数，箭头左侧是函数参数，箭头右侧是函数体。函数的参数类型和返回值类型都可以省略，程序会根据接口定义的上下文自动确定数据类型。
**What is a lambda expression in Java?**
A Lambda expression is just an anonymous function, it is an instance of a functional interface.
**Functional interface**
Single Abstract Method interfaces. From java 8, a new annotation i.e. @FunctionalInterface was introduced.
**lambda expression examples**

1. Iterating over a List and perform some operations

```java
List<String> pointList = new ArrayList();
pointList.add("1");
pointList.add("2");

pointList.forEach(p ->  {
                            System.out.println(p);
                            //Do more work
                        }
                 );
```

2.  Create a new runnable and pass it to thread

```java
new Thread(
    () -> System.out.println("My Runnable");
).start();
```

3. Sorting employees objects by their name

```java
public class LambdaIntroduction {

  public static void main (String[] ar){
          Employee[] employees  = {
              new Employee("David"),
              new Employee("Naveen"),
              new Employee("Alex"),
              new Employee("Richard")};

          System.out.println("Before Sorting Names: "+Arrays.toString(employees));
          Arrays.sort(employees, Employee::nameCompare);
          System.out.println("After Sorting Names "+Arrays.toString(employees));
      }
}

class Employee {
  String name;

  Employee(String name) {
    this.name = name;
  }

  public static int nameCompare(Employee a1, Employee a2) {
    return a1.name.compareTo(a2.name);
  }

  public String toString() {
    return name;
  }
}

Output:

Before Sorting Names: [David, Naveen, Alex, Richard]
After Sorting Names [Alex, David, Naveen, Richard]
```

4. Adding an event listener to a GUI component

```java
JButton button =  new JButton("Submit");
button.addActionListener((e) -> {
    System.out.println("Click event triggered !!");
});
```

## 2. 初识 Stream-API

### 一、什么是 Java Stream API？

Java Stream 函数式编程接口最初是在 Java 8 中引入的，并且与 lambda 一起成为 Java 开发的里程碑式的功能特性，它极大的方便了开放人员处理集合类数据的效率。从笔者之前看过的调查文章显示，绝大部分的开发者使用的 JDK 版本是 java 8，其中 Java Stream 和 lambda 功不可没。

Java Stream 就是一个数据流经的管道，并且在管道中对数据进行操作，然后流入下一个管道。有学过 linux 管道的同学应该会很容易就理解。在没有 Java Stram 之前，对于集合类的操作，更多的是通过 for 循环。大家从后文中就能看出 Java Stream 相对于 for 循环更加简洁、易用、快捷。

管道的功能包括：Filter（过滤）、Map(映射)、sort(排序）等，集合数据通过 Java Stream 管道处理之后，转化为另一组集合或数据输出。
![image](http://cdn.zimug.com/javaStream1-2.jpg)
A Stream in Java can be defined as a sequence of elements from a source that supports aggregate operations on them. The source here refers to a Collections or Arrays who provides data to a Stream.

### 二、Stream API 代替 for 循环

我们先来看一个例子：

```java
List<String> nameStrs = Arrays.asList("Monkey", "Lion", "Giraffe","Lemur");

List<String> list = nameStrs.stream()
        .filter(s -> s.startsWith("L"))
        .map(String::toUpperCase)
        .sorted()
        .collect(toList());
System.out.println(list);
```

- 首先，我们使用 Stream()函数，将一个 List 转换为管道流
- 调用 filter 函数过滤数组元素，过滤方法使用 lambda 表达式，以 L 开头的元素返回 true 被保留，其他的 List 元素被过滤掉
- 然后调用 Map 函数对管道流中每个元素进行处理，字母全部转换为大写
- 然后调用 sort 函数，对管道流中数据进行排序
- 最后调用 collect 函数 toList，将管道流转换为 List 返回

### 三、将数组转换为管道流

使用 Stream.of()方法，将数组转换为管道流。

```java
String[] array = {"Monkey", "Lion", "Giraffe", "Lemur"};
Stream<String> nameStrs2 = Stream.of(array);

Stream<String> nameStrs3 = Stream.of("Monkey", "Lion", "Giraffe", "Lemur");
```

### 四、将集合类对象转换为管道流

通过调用集合类的 stream()方法，将集合类对象转换为管道流。

```java
List<String> list = Arrays.asList("Monkey", "Lion", "Giraffe", "Lemur");
Stream<String> streamFromList = list.stream();

Set<String> set = new HashSet<>(list);
Stream<String> streamFromSet = set.stream();
```

### 五、将文本文件转换为管道流

通过 Files.lines 方法将文本文件转换为管道流，下图中的 Paths.get()方法作用就是获取文件，是 Java NIO 的 API！

也就是说：我们可以很方便的使用 Java Stream 加载文本文件，然后逐行的对文件内容进行处理。

```java
Stream<String> lines = Files.lines(Paths.get("file.txt"));
```

## 3. Stream 的 filter 与谓语逻辑

### 一、基础代码准备

建立一个实体类，该实体类有五个属性。下面的代码使用了 lombok 的注解 Data、AllArgsConstructor，这样我们就不用写 get、set 方法和全参构造函数了。lombok 会帮助我们在编译期生成这些模式化的代码。

```java
@Data
@AllArgsConstructor
public class Employee {

   private Integer id;
   private Integer age;   //年龄
   private String gender;  //性别
   private String firstName;
   private String lastName;
}
```

写一个测试类，这个测试类的内容也很简单，新建十个 Employee 对象

```java
public class StreamFilterPredicate {

    public static void main(String[] args){
        Employee e1 = new Employee(1,23,"M","Rick","Beethovan");
        Employee e2 = new Employee(2,13,"F","Martina","Hengis");
        Employee e3 = new Employee(3,43,"M","Ricky","Martin");
        Employee e4 = new Employee(4,26,"M","Jon","Lowman");
        Employee e5 = new Employee(5,19,"F","Cristine","Maria");
        Employee e6 = new Employee(6,15,"M","David","Feezor");
        Employee e7 = new Employee(7,68,"F","Melissa","Roy");
        Employee e8 = new Employee(8,79,"M","Alex","Gussin");
        Employee e9 = new Employee(9,15,"F","Neetu","Singh");
        Employee e10 = new Employee(10,45,"M","Naveen","Jain");


        List<Employee> employees = Arrays.asList(e1, e2, e3, e4, e5, e6, e7, e8, e9, e10);

        List<Employee> filtered = employees.stream()
                .filter(e -> e.getAge() > 70 && e.getGender().equals("M"))
                .collect(Collectors.toList());

        System.out.println(filtered);

    }

}
```

需要注意的是上面的 filter 传入了 lambda 表达式(之前的章节我们已经讲过了)，表达过滤年龄大于 70 并且男性的 Employee 员工。输出如下：

```java
[Employee(id=8, age=79, gender=M, firstName=Alex, lastName=Gussin)]
```

### 二、什么是谓词逻辑？

下面要说我们的重点了，通过之前的章节的讲解，我们已经知道 lambda 表达式表达的是一个匿名接口函数的实现。那具体到 Stream.filter()中，它表达的是什么呢？看下图：可以看出它表达的是一个 Predicate 接口，在英语中这个单词的意思是：谓词。
![image](https://img.kancloud.cn/94/f0/94f0643476bef3f7d204a41e91949597_810x116.png)
**什么是谓词逻辑？**
WHERE 和 AND 限定了主语 employee 是什么，那么 WHERE 和 AND 语句所代表的逻辑就是谓词逻辑

```java
SELECT *
FROM employee
WHERE age > 70
AND gender = 'M'
```

### 三、谓词逻辑的复用

通常情况下，filter 函数中 lambda 表达式为一次性使用的谓词逻辑。如果我们的谓词逻辑需要被多处、多场景、多代码中使用，通常将它抽取出来单独定义到它所限定的主语实体中。
比如：将下面的谓词逻辑定义在 Employee 实体 class 中。

```java
   public static Predicate<Employee> ageGreaterThan70 = x -> x.getAge() >70;
   public static Predicate<Employee> genderM = x -> x.getGender().equals("M");
```

#### and 语法（并集）

```java
List<Employee> filtered = employees.stream()
        .filter(Employee.ageGreaterThan70.and(Employee.genderM))
        .collect(Collectors.toList());
```

输出如下：

```java
[Employee(id=8, age=79, gender=M, firstName=Alex, lastName=Gussin)]
```

#### or 语法（交集）

```java
List<Employee> filtered = employees.stream()
        .filter(Employee.ageGreaterThan70.or(Employee.genderM))
        .collect(Collectors.toList());
```

输出如下：实际上就是年龄大于 70 的和所有的男性（由于 79 的那位也是男性，所以就是所有的男性）

```java
[Employee(id=1, age=23, gender=M, firstName=Rick, lastName=Beethovan), Employee(id=3, age=43, gender=M, firstName=Ricky, lastName=Martin), Employee(id=4, age=26, gender=M, firstName=Jon, lastName=Lowman), Employee(id=6, age=15, gender=M, firstName=David, lastName=Feezor), Employee(id=8, age=79, gender=M, firstName=Alex, lastName=Gussin), Employee(id=10, age=45, gender=M, firstName=Naveen, lastName=Jain)]
```

#### negate 语法（取反）

```java
List<Employee> filtered = employees.stream()
        .filter(Employee.ageGreaterThan70.or(Employee.genderM).negate())
        .collect(Collectors.toList());
```

输出如下：把上一小节代码的结果取反，实际上就是所有的女性

```java
[Employee(id=2, age=13, gender=F, firstName=Martina, lastName=Hengis), Employee(id=5, age=19, gender=F, firstName=Cristine, lastName=Maria), Employee(id=7, age=68, gender=F, firstName=Melissa, lastName=Roy), Employee(id=9, age=15, gender=F, firstName=Neetu, lastName=Singh)]
```

## 4. Stream 管道流的 map 操作

### 一、回顾 Stream 管道流 map 的基础用法

最简单的需求：将集合中的每一个字符串，全部转换成大写！

```java
List<String> alpha = Arrays.asList("Monkey", "Lion", "Giraffe", "Lemur");

//不使用Stream管道流
List<String> alphaUpper = new ArrayList<>();
for (String s : alpha) {
    alphaUpper.add(s.toUpperCase());
}
System.out.println(alphaUpper); //[MONKEY, LION, GIRAFFE, LEMUR]

// 使用Stream管道流
List<String> collect = alpha.stream().map(String::toUpperCase).collect(Collectors.toList());
//上面使用了方法引用，和下面的lambda表达式语法效果是一样的
//List<String> collect = alpha.stream().map(s -> s.toUpperCase()).collect(Collectors.toList());

System.out.println(collect); //[MONKEY, LION, GIRAFFE, LEMUR]
```

所以 map 函数的作用就是针对管道流中的每一个数据元素进行转换操作。
![image](https://img.kancloud.cn/e4/b3/e4b3980b21802fab8170d9b03422f3ae_1364x632.png)

### 二、处理非字符串类型集合元素

map()函数不仅可以处理数据，还可以转换数据的类型。如下：

```java
List<Integer> lengths = alpha.stream()
        .map(String::length)
        .collect(Collectors.toList());

System.out.println(lengths); //[6, 4, 7, 5]
```

```java
Stream.of("Monkey", "Lion", "Giraffe", "Lemur")
        .mapToInt(String::length)
        .forEach(System.out::println);
```

输出如下：

```java
6
4
7
5
```

除了 mapToInt。还有 maoToLong，mapToDouble 等等用法

### 三、再复杂一点：处理对象数据格式转换

还是使用上一节中的 Employee 类，创建 10 个对象。需求如下：

- 将每一个 Employee 的年龄增加一岁
- 将性别中的“M”换成“male”，F 换成 Female。

```java
public static void main(String[] args){
    Employee e1 = new Employee(1,23,"M","Rick","Beethovan");
    Employee e2 = new Employee(2,13,"F","Martina","Hengis");
    Employee e3 = new Employee(3,43,"M","Ricky","Martin");
    Employee e4 = new Employee(4,26,"M","Jon","Lowman");
    Employee e5 = new Employee(5,19,"F","Cristine","Maria");
    Employee e6 = new Employee(6,15,"M","David","Feezor");
    Employee e7 = new Employee(7,68,"F","Melissa","Roy");
    Employee e8 = new Employee(8,79,"M","Alex","Gussin");
    Employee e9 = new Employee(9,15,"F","Neetu","Singh");
    Employee e10 = new Employee(10,45,"M","Naveen","Jain");


    List<Employee> employees = Arrays.asList(e1, e2, e3, e4, e5, e6, e7, e8, e9, e10);

    /*List<Employee> maped = employees.stream()
            .map(e -> {
                e.setAge(e.getAge() + 1);
                e.setGender(e.getGender().equals("M")?"male":"female");
                return e;
            }).collect(Collectors.toList());*/

    List<Employee> maped = employees.stream()
            .peek(e -> {
                e.setAge(e.getAge() + 1);
                e.setGender(e.getGender().equals("M")?"male":"female");
            }).collect(Collectors.toList());

    System.out.println(maped);

}
```

由于 map 的参数 e 就是返回值，所以可以用 peek 函数。peek 函数是一种特殊的 map 函数，当函数没有返回值或者参数就是返回值的时候可以使用 peek 函数。

### 四、flatMap

map 可以对管道流中的数据进行转换操作，但是如果管道中还有管道该如何处理？即：如何处理二维数组及二维集合类。实现一个简单的需求：将“hello”，“world”两个字符串组成的集合，元素的每一个字母打印出来。如果不用 Stream 我们怎么写？写 2 层 for 循环,第一层遍历字符串，并且将字符串拆分成 char 数组，第二层 for 循环遍历 char 数组。

```java
List<String> words = Arrays.asList("hello", "word");
words.stream()
        .map(w -> Arrays.stream(w.split("")))    //[[h,e,l,l,o],[w,o,r,l,d]]
        .forEach(System.out::println);

```

输出打印结果：

```java
java.util.stream.ReferencePipeline$Head@3551a94
java.util.stream.ReferencePipeline$Head@531be3c5
```

- 用 map 方法是做不到的，这个需求用 map 方法无法实现。map 只能针对一维数组进行操作，数组里面还有数组，管道里面还有管道，它是处理不了每一个元素的。
  ![image](https://img.kancloud.cn/93/8a/938a9ceb8f8bd52a92111d1112e1b7e6_1256x524.png)
- flatMap 可以理解为将若干个子管道中的数据全都，平面展开到父管道中进行处理。
  ![image](https://img.kancloud.cn/52/55/5255f59f26e472cd30314bbd1e243e73_1198x498.png)

```java
words.stream()
        .flatMap(w -> Arrays.stream(w.split(""))) // [h,e,l,l,o,w,o,r,l,d]
        .forEach(System.out::println);
```

输出打印结果：

```java
h
e
l
l
o
w
o
r
d
```

## 5.Stream 的状态与并行操作

### 一、回顾 Stream 管道流操作

![image](https://img.kancloud.cn/87/80/8780fbf2c447fbf574591cab30cb743c_631x282.png)
通过前面章节的学习，我们应该明白了 Stream 管道流的基本操作。我们来回顾一下：

- 源操作：可以将数组、集合类、行文本文件转换成管道流 Stream 进行数据处理
- 中间操作：对 Stream 流中的数据进行处理，比如：过滤、数据转换等等
- 终端操作：作用就是将 Stream 管道流转换为其他的数据类型。这部分我们还没有讲，我们后面章节再介绍

看下面的脑图，可以有更清晰的理解：
![image](https://img.kancloud.cn/78/f7/78f74991175f6ddc5c27fff109f0fc66_942x578.png)

### 二、中间操作：有状态与无状态

其实在程序员编程中，经常会接触到“有状态”，“无状态”，绝大部分的人都比较蒙。而且在不同的场景下，“状态”这个词的含义似乎有所不同。但是“万变不离其宗”，理解“状态”这个词在编程领域的含义，笔者教给大家几个关键点

- 状态通常代表公用数据，有状态就是有“公用数据”
- 因为有公用的数据，状态通常需要额外的存储。
- 状态通常被多人、多用户、多线程、多次操作，这就涉及到状态的管理及变更操作。

是不是更蒙了？举个例子，你就明白了

- web 开发 session 就是一种状态，访问者的多次请求关联同一个 session，这个 session 需要存储到内存或者 redis。多次请求使用同一个公用的 session，这个 session 就是状态数据。
- vue 的 vuex 的 store 就是一种状态，首先它是多组件公用的，其次是不同的组件都可以修改它，最后它需要独立于组件单独存储。所以 store 就是一种状态。

回到我们的 Stream 管道流

- filter 与 map 操作，不需要管道流的前面后面元素相关，所以不需要额外的记录元素之间的关系。输入一个元素，获得一个结果。
- sorted 是排序操作、distinct 是去重操作。像这种操作都是和别的元素相关的操作，我自己无法完成整体操作。就像班级点名就是无状态的，喊到你你就答到就可以了。如果是班级同学按大小个排序，那就不是你自己的事了，你得和周围的同学比一下身高并记住，你记住的这个身高比较结果就是一种“状态”。所以这种操作就是有状态操作。

### 三、Limit 与 Skip 管道数据截取

```java
List<String> limitN = Stream.of("Monkey", "Lion", "Giraffe", "Lemur")
        .limit(2)
        .collect(Collectors.toList());
List<String> skipN = Stream.of("Monkey", "Lion", "Giraffe", "Lemur")
        .skip(2)
        .collect(Collectors.toList());
```

- limt 方法传入一个整数 n，用于截取管道中的前 n 个元素。经过管道处理之后的数据是：[Monkey, Lion]。
- skip 方法与 limit 方法的使用相反，用于跳过前 n 个元素，截取从 n 到末尾的元素。经过管道处理之后的数据是： [Giraffe, Lemur]

### 四、Distinct 元素去重

我们还可以使用 distinct 方法对管道中的元素去重，涉及到去重就一定涉及到元素之间的比较，distinct 方法时调用 Object 的 equals 方法进行对象的比较的，如果你有自己的比较规则，可以重写 equals 方法。

```java
List<String> uniqueAnimals = Stream.of("Monkey", "Lion", "Giraffe", "Lemur", "Lion")
        .distinct()
        .collect(Collectors.toList());
```

上面代码去重之后的结果是： ["Monkey", "Lion", "Giraffe", "Lemur"]

### 五、Sorted 排序

默认的情况下，sorted 是按照字母的自然顺序进行排序。如下代码的排序结果是：[Giraffe, Lemur, Lion, Monkey]，字数按顺序 G 在 L 前面，L 在 M 前面。第一位无法区分顺序，就比较第二位字母。

```java
List<String> alphabeticOrder = Stream.of("Monkey", "Lion", "Giraffe", "Lemur")
        .sorted()
        .collect(Collectors.toList());
```

排序我们后面还会给大家详细的讲一讲，所以这里暂时只做一个了解。

### 六、串行、并行与顺序

通常情况下，有状态和无状态操作不需要我们去关心。除非？：你使用了并行操作。

还是用班级按身高排队为例：班级有一个人负责排序，这个排序结果最后就会是正确的。那如果有 2 个、3 个人负责按大小个排队呢？最后可能就乱套了。一个人只能保证自己排序的人的顺序，他无法保证其他人的排队顺序。

- 串行的好处是可以保证顺序，但是通常情况下处理速度慢一些
- 并行的好处是对于元素的处理速度快一些（通常情况下），但是顺序无法保证。这可能会导致进行一些有状态操作的时候，最后得到的不是你想要的结果。
  ![image](https://img.kancloud.cn/92/39/92394040fe48efd292feca03fa9da193_662x356.png)

```java
Stream.of("Monkey", "Lion", "Giraffe", "Lemur", "Lion")
        .parallel()
        .forEach(System.out::println);
```

- parallel()函数表示对管道中的元素进行并行处理，而不是串行处理。但是这样就有可能导致管道流中后面的元素先处理，前面的元素后处理，也就是元素的顺序无法保证。
  > 如果数据量比较小的情况下，不太能观察到，数据量大的话，就能观察到数据顺序是无法保证的。

```java
Monkey
Lion
Lemur
Giraffe
Lion
```

通常情况下，parallel()能够很好的利用 CPU 的多核处理器，达到更好的执行效率和性能，建议使用。但是有些特殊的情况下，parallel 并不适合：深入了解请看这篇文章：
https://blog.oio.de/2016/01/22/parallel-stream-processing-in-java-8-performance-of-sequential-vs-parallel-stream-processing/
该文章中几个观点，说明并行操作的适用场景：

- 数据源易拆分：从处理性能的角度，parallel()更适合处理 ArrayList，而不是 LinkedList。因为 ArrayList 从数据结构上讲是基于数组的，可以根据索引很容易的拆分为多个。
  ![image](https://img.kancloud.cn/2d/85/2d85dbdaf34057b0fb5bf800f632b695_799x471.png)
- 适用于无状态操作：每个元素的计算都不得依赖或影响任何其他元素的计算，的运算场景。
- 基础数据源无变化：从文本文件里面边读边处理的场景，不适合 parallel()并行处理。parallel()一开始就容量固定的集合，这样能够平均的拆分、同步处理。
