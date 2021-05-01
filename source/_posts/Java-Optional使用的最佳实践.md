---
title: Java Optional使用的最佳实践
date: 2020-08-10 15:06:51
tags:
---
Optional隐藏了可能存在空指针的不确定性，比如：
```java
List<String> numbers= ImmutableList.of("ONE", "TWO", "THREE");

return numbers.stream()
 .filter(number -> "FOUR".equals(number))
 .findAny()
 .toLoweCase();
 ```
 结果会导致NullPointerExceptions空指针错误，而使用if else进行判断是一种切割器cutter味道：
 ```java
 List<String> numbers= ImmutableList.of("ONE", "TWO", "THREE");
String numberThatImLookingFour = 
numbers.stream()
 .filter(number -> "FOUR".equals(number))
 .findAny();
if(numberThatImLookingFour != null){
 return numberThatImLookingFour.toLowerCase();
}else{
 return "not found";
}
```
所以Brian Goetz和Steward Marks（Java语言架构师）聚在一起写下了以下段落：

我们的目的是为库方法的返回类型提供一种有限的机制，其中需要一种明确的方式来表示“无结果”，并且对于这样的方法使用null绝对可能导致错误。

因此添加了Optional <T>，这不是一个真正的新概念，历史可以追溯到Haskell的Maybe monad。突然间，我们获得了JDK批准的表示可能存在或不存在的值的方式，和往常一样，在各地使用新功能的开发人员抓狂了。

空引用空指针是无数个错误的来源，通常也不能很好地标识“不存在”这个概念。

应该如何处理这个问题的重要部分来自DDD。在有界上下文的入口处我们说：' 你不能通过 '：

传入领域的所有变量是执行业务逻辑所需的，我们必须减少编写if（obj == null）检查判断的代码行数量。我们仍然需要与外部世界（数据库查询，REST端点等）进行交互，并根据执行的逻辑交互输出。如果使用Optional 得当则可以提供帮助。

**什么是Optional?**

- 它是box类型，保持对另一个对象的引用。
- 是不可变的，不可序列化的
- 没有公共构造函数
- 只能是present 或absent
- 通过of(), ofNullable(), empty() 静态方法创建。

**从这个盒子box中如何获取值？**

- get()
- orElse()
- orElseGet()
- orElseThrow()

有一种诱惑是调用get()来获取其中的值。我们都知道普通JavaBean的getter / setters :)。并且期望如果我们调用get ...（）我们就会得到一些东西。当调用普通bean的getter时，你永远不会得到任何抛出的异常。但是，如果调用在optional上调用get方法，并且该选项内部为空时，则会抛出异常NoSuchElementException。

这些方法应该被称为getOrThorwSomeHorribleError()，因此第一和第二条规则：

**＃1不要将null赋给Optional**

**＃2避免使用Optional.get()。如果你不能证明存在可选项，那么永远不要调用get（）**。
使用orElse(), orElseGet(), orElseThrow().获得你的结果。

可以重构以下代码：
```java
String variable = fetchSomeVaraible();
if(variable == null){
 1. throw new IllegalStateException("No such variable");
 2. return createVariable();
 3. return "new variable";
} else { 
 ... 
 100 lines of code
 ...
}
```
重构到:
```java
1. 
Optional<String> variableOpt = fetchOptionalSomeVaraible();
String variable = variableOpt.orElseThrow(() -> new Exeption("")) 
... 100 lines of code ...
2.
Optional<String> variableOpt = fetchOptionalSomeVaraible();
String variable = variableOpt.orElseGet(() -> createVariable()) 
... 100 lines of code ...
3.
Optional<String> variableOpt = fetchOptionalSomeVaraible();
String variable = variableOpt.orElse("new variable") 
... 100 lines of code ...
```
注意，orElse(..)是急切计算，意味着下面代码：
```java
Optional<Dog> optionalDog = fetchOptionalDog();
optionalDog
 .map(this::printUserAndReturnUser)
 .orElse(this::printVoidAndReturnUser)
```
如果值存在则将执行两个方法，如果值不存在，则仅执行最后一个方法。为了处理这些情况，我们可以使用方法orElseGet（），它将supplier 作为参数，并且是惰性计算的。

**＃3不要在字段，方法参数，集合中使用Optional。**
下面是将thatField直接赋值给了类字段：
```java
public void setThatField（Optional <ThatFieldType> thatField）{ 
  this.thatField = thatField; 
} 
```
改为：
```java
setThatField（Optional.ofNullable（thatField））;
```
**＃4只有每当结果不确定时，使用Optional作为返回类型。。**
说实话，这是使用Optional的唯一好地方。我将复制粘贴前面的话：

我们的目的是为库方法的返回类型提供一种有限的机制，其中需要一种明确的方式来表示“无结果”，并且对于这样的方法使用null 绝对可能导致错误。
**＃5不要害怕使用map和filter。**
有一些值得遵循的一般开发实践称为SLA-p：Single Layer of Abstraction字母的第一个大写。

下面是需要被重构代码：
```java
Dog dog = fetchSomeVaraible();
String dogString = dogToString(dog);
public String dogToString(Dog dog){
 if(dog == null){
   return "DOG'd name is : " + dog.getName();
 } else { 
   return "CAT";
 }
}
```
重构到：
```java

Optional<Dog> dog = fetchDogIfExists();
String dogsName = dog
 .map(this::convertToDog)
 .orElseGet(this::convertToCat)
public void convertToDog(Dog dog){
   return "DOG'd name is : " + dog.getName();
}
public void convertToCat(){
   return "CAT";
}
```
Filter是有用的折叠语法：
```java
Dog dog = fetchDog();
if(optionalDog != null && optionalDog.isBigDog()){
  doBlaBlaBla(optionalDog);
}

```
上面代码可以被重构为：
```java
Optional<Dog> optionalDog = fetchOptionalDog();
optionalDog
 .filter(Dog::isBigDog)
 .ifPresent(this::doBlaBlaBla)
 ```
 **＃6不要为了链方法而使用optional 。**
 使用optional 时要注意的一件事是链式方法的诱惑。当我们像构建器模式一样链接方法时，事情可能看起来很漂亮:)。但并不总是等于更具可读性。所以不要这样做：
```java

Optional
 .ofNullable(someVariable)
 .ifPresent(this::blablabla)
```
它对性能不利，对可读性也不好。我们应尽可能避免使用null引用。
**＃7使所有表达式成为单行lambda**

这是更普遍的规则，我认为也应该应用于流。但这篇文章是关于optional 。使用Optional 重要点是记住等式左边和右边一样重要：
```java
Optional
 .ofNullable(someVariable)
 .map(variable -> {
   try{
      return someREpozitory.findById(variable.getIdOfOtherObject());
   } catch (IOException e){
     LOGGER.error(e); 
     throw new RuntimeException(e); 
   }})
 .filter(variable -> { 
   if(variable.getSomeField1() != null){
     return true;
   } else if(variable.getSomeField2() != null){
     return false;   
   } else { 
     return true;
   }
  })
 .map((variable -> {
   try{
      return jsonMapper.toJson(variable);
   } catch (IOException e){
     LOGGER.error(e); 
     throw new RuntimeException(e); 
   }}))
 .map(String::trim)
 .orElseThrow(() -> new RuntimeException("something went horribly wrong."))
```
上面那么冗长代码块可以使用方法替代：
```java
Optional
 .ofNullable(someVariable)
 .map(this::findOtherObject)
 .filter(this::isThisOtherObjectStale)
 .map(this::convertToJson)
 .map(String::trim)
 .orElseThrow(() -> new RuntimeException("something went horribly wrong."));
```

