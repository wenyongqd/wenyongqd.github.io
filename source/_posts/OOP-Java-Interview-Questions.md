---
layout: post
title: OOP Java Interview Questions
subtitle: "\"Anyone can be cool, but awesome take practice.\""
date: 2020-03-13 19:31:33
tags:
    - Interview
---
> This document is not completed and will be updated anytime.

1. [What is polymorphism](#What-is-polymorphism)
2. [What is runtime polymorphism or dynamic method dispatch](#Runtime-Polymorphism-in-Java)
3. [What is abstraction in Java](#Abstract-class-in-Java)
4. [What do you mean by an interface in Java](#Interface-in-Java)

> Practise Hard

![bruce](https://miro.medium.com/max/992/1*-R5r7bEBUU2nmPXI5WD_dQ.jpeg)
---
## What is polymorphism
**Polymorphism** is the ability of an object to take on many forms. The most common use of polymorphism in OOP occurs when a parent class reference is used to refer to a child class object.

If a child class override a method in its parent, an overriden method is essentially hidden in the parent class, and is not invoked unless the child class uses the super keyword within the overriding method. That means the same type reference variable perform a single action in different ways, this is polymorphism.

There are two types of polymorphism in Java: **compile-time polymorphism** and **runtime polymorphism**. We can perform polymorphism in java by method overloading and method overriding.

#### Runtime Polymorphism in Java
**Runtime polymorphism** or **Dynamic Method Dispatch** is a process in which a call to an overridden method is resolved at runtime rather than compile-time.

In this process, an overridden method is called through the reference variable of a superclass. The determination of the method to be called is based on the object being referred to by the reference variable.
##### Upcasting
If the reference variable of Parent class refers to the object of Child class, it is known as upcasting. For example:
![java-upcasting](https://static.javatpoint.com/images/java-upcasting.png)
```java
class A{}  
class B extends A{}  
```
```java
A a=new B();//upcasting  
```
For upcasting, we can use the reference variable of class type or an interface type. For Example:
```java
interface I{}  
class A{}  
class B extends A implements I{} 
```
Here, the relationship of B class would be:
```java
B IS-A A
B IS-A I
B IS-A Object
```
#### Example of Java Runtime Polymorphism
Consider a scenario where Bank is a class that provides a method to get the rate of interest. However, the rate of interest may differ according to banks. For example, SBI, ICICI, and AXIS banks are providing 8.4%, 7.3%, and 9.7% rate of interest.
![Bank](https://static.javatpoint.com/images/core/bankinheritance.png)
> Note: This example is also given in method overriding but there was no upcasting.

```java
class Bank{  
float getRateOfInterest(){return 0;}  
}  
class SBI extends Bank{  
float getRateOfInterest(){return 8.4f;}  
}  
class ICICI extends Bank{  
float getRateOfInterest(){return 7.3f;}  
}  
class AXIS extends Bank{  
float getRateOfInterest(){return 9.7f;}  
}  
class TestPolymorphism{  
public static void main(String args[]){  
Bank b;  
b=new SBI();  
System.out.println("SBI Rate of Interest: "+b.getRateOfInterest());  
b=new ICICI();  
System.out.println("ICICI Rate of Interest: "+b.getRateOfInterest());  
b=new AXIS();  
System.out.println("AXIS Rate of Interest: "+b.getRateOfInterest());  
}  
}
```
Output:
```java
SBI Rate of Interest: 8.4
ICICI Rate of Interest: 7.3
AXIS Rate of Interest: 9.7
```
#### Java Runtime Polymorphism with Data Member
A method is overridden, not the data members, so runtime polymorphism can't be achieved by data members.

In the example given below, both the classes have a data member speedlimit. We are accessing the data member by the reference variable of Parent class which refers to the subclass object. Since we are accessing the data member which is not overridden, hence it will access the data member of the Parent class always.
> Rule: Runtime polymorphism can't be achieved by data members.

```java
class Bike{  
 int speedlimit=90;  
}  
class Honda3 extends Bike{  
 int speedlimit=150;  
  
 public static void main(String args[]){  
  Bike obj=new Honda3();  
  System.out.println(obj.speedlimit);//90  
}
```
Output:
```java
90
```
#### Java Runtime Polymorphism with Multilevel Inheritance
Let's see the simple example of Runtime Polymorphism with multilevel inheritance.
```java
class Animal{  
    void eat(){System.out.println("eating");}  
}  
class Dog extends Animal{  
    void eat(){System.out.println("eating fruits");}  
}  
class BabyDog extends Dog{  
    void eat(){System.out.println("drinking milk");}  
    public static void main(String args[]){  
    Animal a1,a2,a3;  
    a1=new Animal();  
    a2=new Dog();  
    a3=new BabyDog();  
    a1.eat();  
    a2.eat();  
    a3.eat();  
    }  
}  
```
Output:
```java
eating
eating fruits
drinking Milk
```
---
## Abstract class in Java
A class which is declared with the abstract keyword is known as an abstract class in Java. It can have abstract and non-abstract methods (method with the body).

Abstraction refers to the quality of dealing with ideas rather than events. It basically deals with hiding the details and showing the essential things to the user. Thus you can say that abstraction in Java is the process of hiding the implementation details from the user and revealing only the functionality to them. Abstraction can be achieved in two ways:

1. **Abstract Classes** (0-100% of abstraction can be achieved)
2. **Interfaces** (100% of abstraction can be achieved)

#### Abstraction in Java
**Abstraction** is a process of hiding the implementation details and showing only functionality to the user.

Another way, it shows only essential things to the user and hides the internal details, for example, sending SMS where you type the text and send the message. You don't know the internal processing about the message delivery.

Abstraction lets you focus on what the object does instead of how it does it.
#### Ways to achieve Abstraction
There are two ways to achieve abstraction in java

1. Abstract class (0 to 100%)
2. Interface (100%)

##### Points to Remember
- An abstract class must be declared with an abstract keyword.
- It can have abstract and non-abstract methods.
- It cannot be instantiated.
- It can have constructors and static methods also.
- It can have final methods which will force the subclass not to change the body of the method.
![Abstract](https://static.javatpoint.com/images/abstract-class-in-java.jpg)

#### Understanding the real scenario of Abstract class
In this example, Shape is the abstract class, and its implementation is provided by the Rectangle and Circle classes.

Mostly, we don't know about the implementation class (which is hidden to the end user), and an object of the implementation class is provided by the **factory method**.

**A factory method** is a method that returns the instance of the class. We will learn about the factory method later.

In this example, if you create the instance of Rectangle class, draw() method of Rectangle class will be invoked.

```java
abstract class Shape{  
    abstract void draw();  
}  
//In real scenario, implementation is provided by others i.e. unknown by end user  
class Rectangle extends Shape{  
    void draw(){System.out.println("drawing rectangle");}  
}  
class Circle1 extends Shape{  
    void draw(){System.out.println("drawing circle");}  
}  
//In real scenario, method is called by programmer or user  
class TestAbstraction1{  
    public static void main(String args[]){  
        Shape s=new Circle1();//In a real scenario, object is provided through method, e.g., getShape() method  
        s.draw();  
    }  
}
```
```java
Rate of Interest is: 7 %
Rate of Interest is: 8 %
```

#### Abstract class having constructor, data member and methods
An abstract class can have a data member, abstract method, method body (non-abstract method), constructor, and even main() method.
```java
//Example of an abstract class that has abstract and non-abstract methods  
 abstract class Bike{ 
    Bike(){System.out.println("bike is created");}  
    abstract void run();  
    void changeGear(){System.out.println("gear changed");}  
 }  
//Creating a Child class which inherits Abstract class  
class Honda extends Bike{  
    void run(){System.out.println("running safely..");}  
 }  
//Creating a Test class which calls abstract and non-abstract methods  
class TestAbstraction2{  
    public static void main(String args[]){  
    Bike obj = new Honda();  
    obj.run();  
    obj.changeGear();  
    }  
}  
```
```java
bike is created
running safely..
gear changed
```
> Rule: If there is an abstract method in a class, that class must be abstract.

> Rule: If you are extending an abstract class that has an abstract method, you must either provide the implementation of the method or make this class abstract.

## Interface in Java
An **interface in Java** is a blueprint of a class. It has static constants and abstract methods.

The interface in Java is a mechanism to achieve abstraction. There can be only abstract methods in the Java interface, not method body. It is used to achieve abstraction and multiple inheritance in Java.

In other words, you can say that interfaces can have abstract methods and variables. It cannot have a method body.

#### Why use Java interface?
There are mainly three reasons to use interface. They are given below.

- It is used to achieve abstraction.
- By interface, we can support the functionality of multiple inheritance.
- It can be used to achieve loose coupling.

## What is abstraction in Java

![interface](https://static.javatpoint.com/interview/images/why-use-java-interface.jpg)