---
title: Java Interview Questions
date: 2020-04-14 11:35:35
tags:
  - Interview
---

<!-- TOC -->

- [Q1. What are wrapper classes in Java?](#q1-what-are-wrapper-classes-in-java)
- [Q2. What are constructors in Java?](#q2-what-are-constructors-in-java)
- [Q3. What is singleton class in Java and how can we make a class singleton?](#q3-what-is-singleton-class-in-java-and-how-can-we-make-a-class-singleton)
- [Q4. What is the difference between Array list and vector in Java?](#q4-what-is-the-difference-between-array-list-and-vector-in-java)
- [Q5. What is the difference between equals() and == in Java?](#q5-what-is-the-difference-between-equals-and--in-java)
- [Q6. What are the differences between Heap and Stack Memory in Java?](#q6-what-are-the-differences-between-heap-and-stack-memory-in-java)
  - [Java Heap Space](#java-heap-space)
  - [Java Stack Memory](#java-stack-memory)
  - [Heap and Stack Memory in Java Program](#heap-and-stack-memory-in-java-program)
  - [Difference between Java Heap Space and Stack Memory](#difference-between-java-heap-space-and-stack-memory)
- [Q7. Why pointers are not used in Java?](#q7-why-pointers-are-not-used-in-java)
- [Q8. What are access modifiers in Java?](#q8-what-are-access-modifiers-in-java)
- [Q9 How garbage collector knows that the object is not in use and needs to be removed?](#q9-how-garbage-collector-knows-that-the-object-is-not-in-use-and-needs-to-be-removed)
- [Q10 Can Java thread object invoke start method twice?](#q10-can-java-thread-object-invoke-start-method-twice)
- [Q11 Give the list of Java Object class methods.](#q11-give-the-list-of-java-object-class-methods)
- [Q12 Can we override static method?](#q12-can-we-override-static-method)
- [Q13 Can you list serialization methods?](#q13-can-you-list-serialization-methods)
- [Q14 What is the difference between super() and this()?](#q14-what-is-the-difference-between-super-and-this)
- [Q15 How to prevent a method from being overridden?](#q15-how-to-prevent-a-method-from-being-overridden)
- [Q16 Can we create abstract classes without any abstract methods?](#q16-can-we-create-abstract-classes-without-any-abstract-methods)
- [Q17 How to destroy the session in servlets?](#q17-how-to-destroy-the-session-in-servlets)
- [Q18 Explain Final keyword in java?](#q18-explain-final-keyword-in-java)
- [Q19 When is the super keyword used?](#q19-when-is-the-super-keyword-used)
- [Q20 What is the difference between StringBuffer and String?](#q20-what-is-the-difference-between-stringbuffer-and-string)
- [Q21 Why multiple inheritance is not supported in java?](#q21-why-multiple-inheritance-is-not-supported-in-java)
- [Q22 What is the difference between ‘throw’ and ‘throws’ in Java Exception Handling?](#q22-what-is-the-difference-between-throw-and-throws-in-java-exception-handling)
- [Q23 What is finalize() method?](#q23-what-is-finalize-method)
- [Q24 Difference in Set and List interface?](#q24-difference-in-set-and-list-interface)
- [Q25 What will happen if you put System.exit(0) on try or catch block? Will finally block execute?](#q25-what-will-happen-if-you-put-systemexit0-on-try-or-catch-block-will-finally-block-execute)
- [Q26 Overriding vs. Overloading](#q26-overriding-vs-overloading)
- [Q27 String vs StringBuffer vs StringBuilder](#q27-string-vs-stringbuffer-vs-stringbuilder)
- [Q27 Autoboxing and Unautoboxing in Java](#q27-autoboxing-and-unautoboxing-in-java)
- [Q28 Exception Handling in Java](#q28-exception-handling-in-java)
- [Q29 What is the difference between Checked and Unchecked Exception in Java?](#q29-what-is-the-difference-between-checked-and-unchecked-exception-in-java)
- [Q30 获取用键盘输入常用的的两种方法](#q30-获取用键盘输入常用的的两种方法)
- [Q31 Difference between abstract class and interface](#q31-difference-between-abstract-class-and-interface)
- [Q32 What is Inheritance in Java?](#q32-what-is-inheritance-in-java)
- [Q32 What are different types of Inheritance supported by Java?](#q32-what-are-different-types-of-inheritance-supported-by-java)
- [Q32 Why multiple Inheritance is not supported by Java?](#q32-why-multiple-inheritance-is-not-supported-by-java)
- [Q33 What is the difference between Inheritance and Abstraction?](#q33-what-is-the-difference-between-inheritance-and-abstraction)
- [Q34 Can we override static method in Java?](#q34-can-we-override-static-method-in-java)
- [Q35 The four principles of object-oriented programming are encapsulation, abstraction, inheritance, and polymorphism](#q35-the-four-principles-of-object-oriented-programming-are-encapsulation-abstraction-inheritance-and-polymorphism)
- [Q36 Multithreading and Life Cycle of a thread](#q36-multithreading-and-life-cycle-of-a-thread)
- [Q37 What id Thread Synchronization?](#q37-what-id-thread-synchronization)
- [Q38 Handling thread deadlock?](#q38-handling-thread-deadlock)
- [Q39 What is Thread Safty?](#q39-what-is-thread-safty)
- [Q40 What is Concurrency?](#q40-what-is-concurrency)
- [Difference between Runnable vs Thread in Java](#difference-between-runnable-vs-thread-in-java)
  - [1. Create Thread using Runnable Interface vs Thread class](#1-create-thread-using-runnable-interface-vs-thread-class)
    - [1.1. Runnable interface](#11-runnable-interface)
    - [1.2. Thread class](#12-thread-class)
  - [2. Difference between Runnable vs Thread](#2-difference-between-runnable-vs-thread)
- [Q41 What is a thread local variable?](#q41-what-is-a-thread-local-variable)
- [Q42 What is the difference between sleep and wait?](#q42-what-is-the-difference-between-sleep-and-wait)
- [Q43 What is the difference between notify() and notifyAll()?](#q43-what-is-the-difference-between-notify-and-notifyall)
- [Q44 What are the different thread states?](#q44-what-are-the-different-thread-states)
- [Q45 What is the difference between thread and process?](#q45-what-is-the-difference-between-thread-and-process)
- [Q46 How do we create thread in Java?](#q46-how-do-we-create-thread-in-java)
- [Q47 Difference between Vector and ArrayList?](#q47-difference-between-vector-and-arraylist)
- [Q48 Difference between HashMap and HashTable?](#q48-difference-between-hashmap-and-hashtable)
- [Q49 Difference between Set and List?](#q49-difference-between-set-and-list)
- [Q50 How to design a good key for hashmap?](#q50-how-to-design-a-good-key-for-hashmap)
- [Q51 How hashmap works?](#q51-how-hashmap-works)
- [What is REST?](#what-is-rest)

<!-- /TOC -->

### Q1. What are wrapper classes in Java?

Wrapper classes convert the Java primitives into the reference types (objects). Every primitive data type has a class dedicated to it. These are known as wrapper classes because they “wrap” the primitive data type into an object of that class. Refer to the below image which displays different primitive type, wrapper class and constructor argument.
![day1](d1.png)

### Q2. What are constructors in Java?

In Java, constructor refers to a block of code which is used to initialize an object. It must have the same name as that of the class. Also, it has no return type and it is automatically called when an object is created.

There are two types of constructors:

- **Default Constructor**: In Java, a default constructor is the one which does not take any inputs. In other words, default constructors are the no argument constructors which will be created by default in case no other constructor is defined by the user. Its **main purpose** is to initialize the instance variables with the default values. Also, it is majorly used for object creation.
- **Parameterized Constructor**: The parameterized constructor in Java, is the constructor which is capable of initializing the instance variables with the provided values. In other words, the constructors which take the arguments are called parameterized constructors.

### Q3. What is singleton class in Java and how can we make a class singleton?

Singleton class means you can create only one object for the given class. You can create a singleton class by making its constructor as private, so that you can restrict the creation of the object. Provide a static method to get instance of the object, wherein you can handle the object creation inside the class only. In this example we are creating object by using static block.

```java
ublic class MySingleton {

    private static MySingleton myObj;

    static{
        myObj = new MySingleton();
    }

    private MySingleton(){

    }

    public static MySingleton getInstance(){
        return myObj;
    }

    public void testMe(){
        System.out.println("Hey.... it is working!!!");
    }

    public static void main(String a[]){
        MySingleton ms = getInstance();
        ms.testMe();
    }
}
```

### Q4. What is the difference between Array list and vector in Java?

![d2](d2.png)

### Q5. What is the difference between equals() and == in Java?

In general both equals() and “==” operator in Java are used to compare objects to check equality but here are some of the differences between the two:

1. First difference between them is, equals() is a method defined inside the java.lang.Object class and == is one type of operator and you can compare both primitive and objects using equality operator in Java.

2. We can use == operators for reference comparison (address comparison) and .equals() method for content comparison. In simple words, == checks if both objects point to the same memory location whereas .equals() evaluates to the comparison of values in the objects.
3. If a class does not override the equals method, then by default it uses equals(Object o) method of the closest parent class that has overridden this method. See this for detail
   Coding Example:

```java
// Java program to understand
// the concept of == operator
public class Test {
    public static void main(String[] args)
    {
        String s1 = new String("HELLO");
        String s2 = new String("HELLO");
        System.out.println(s1 == s2);
        System.out.println(s1.equals(s2));
    }
}
```

```shell script
false
true

```

### Q6. What are the differences between Heap and Stack Memory in Java?

#### Java Heap Space

Java Heap space is used by java runtime to allocate memory to Objects and JRE classes. Whenever we create an object, it’s always created in the Heap space.

Garbage Collection runs on the heap memory to free the memory used by objects that don’t have any reference. Any object created in the heap space has global access and can be referenced from anywhere of the application.
https://www.journaldev.com/4098/java-heap-space-vs-stack-memory

#### Java Stack Memory

Java Stack memory is used for the execution of a thread. They contain method-specific values that are short-lived and references to other objects in the heap that is getting referred from the method.

Stack memory is always referenced in LIFO (Last-In-First-Out) order. Whenever a method is invoked, a new block is created in the stack memory for the method to hold local primitive values and reference to other objects in the method.

As soon as the method ends, the block becomes unused and becomes available for the next method.
Stack memory size is very less compared to Heap memory.

#### Heap and Stack Memory in Java Program

Let’s understand the Heap and Stack memory usage with a simple program.

```java
package com.journaldev.test;

public class Memory {

	public static void main(String[] args) { // Line 1
		int i=1; // Line 2
		Object obj = new Object(); // Line 3
		Memory mem = new Memory(); // Line 4
		mem.foo(obj); // Line 5
	} // Line 9

	private void foo(Object param) { // Line 6
		String str = param.toString(); //// Line 7
		System.out.println(str);
	} // Line 8

}

```

Let’s go through the steps of the execution of the program.

- As soon as we run the program, it loads all the Runtime classes into the Heap space. When the main() method is found at line 1, Java Runtime creates stack memory to be used by main() method thread.
- We are creating primitive local variable at line 2, so it’s created and stored in the stack memory of main() method.
- Since we are creating an Object in the 3rd line, it’s created in heap memory and stack memory contains the reference for it. A similar process occurs when we create Memory object in the 4th line.
- Now when we call the foo() method in the 5th line, a block in the top of the stack is created to be used by the foo() method. Since Java is pass-by-value, a new reference to Object is created in the foo() stack block in the 6th line.
- A string is created in the 7th line, it goes in the String Pool in the heap space and a reference is created in the foo() stack space for it.
- foo() method is terminated in the 8th line, at this time memory block allocated for foo() in stack becomes free.
- In line 9, main() method terminates and the stack memory created for main() method is destroyed. Also, the program ends at this line, hence Java Runtime frees all the memory and ends the execution of the program.
  ![image](https://cdn.journaldev.com/wp-content/uploads/2014/08/Java-Heap-Stack-Memory.png)

#### Difference between Java Heap Space and Stack Memory

Based on the above explanations, we can easily conclude the following differences between Heap and Stack memory.

1. Heap memory is used by all the parts of the application whereas stack memory is used only by one thread of execution.
2. Whenever an object is created, it’s always stored in the Heap space and stack memory contains the reference to it. Stack memory only contains local primitive variables and reference variables to objects in heap space.
3. Objects stored in the heap are globally accessible whereas stack memory can’t be accessed by other threads.
4. Memory management in stack is done in LIFO manner whereas it’s more complex in Heap memory because it’s used globally. Heap memory is divided into Young-Generation, Old-Generation etc, more details at Java `Garbage Collection`.
5. Stack memory is short-lived whereas heap memory lives from the start till the end of application execution.
6. We can use -Xms and -Xmx JVM option to define the startup size and maximum size of heap memory. We can use -Xss to define the stack memory size.
7. When stack memory is full, Java runtime throws `java.lang.StackOverFlowError` whereas if heap memory is full, it throws `java.lang.OutOfMemoryError`: Java Heap Space error.
8. Stack memory size is very less when compared to Heap memory. Because of simplicity in memory allocation (LIFO), stack memory is very fast when compared to heap memory.

### Q7. Why pointers are not used in Java?

Java doesn’t use pointers because they are unsafe and increases the complexity of the program. Since, Java is known for its simplicity of code, adding the concept of pointers will be contradicting. Moreover, since JVM is responsible for implicit memory allocation, thus in order to avoid direct access to memory by the user, pointers are discouraged in Java.
Q

### Q8. What are access modifiers in Java?

As the name suggests access modifiers in Java helps to restrict the scope of a class, constructor , variable , method or data member. There are four types of access modifiers available in java:

1. Default – No keyword required
   **Default**: When no access modifier is specified for a class , method or data member – It is said to be having the default access modifier by default.
2. Private
   **Private**: The private access modifier is specified using the keyword private.

   - The methods or data members declared as private are accessible only within the class in which they are declared.
   - Any other class of same package will not be able to access these members.
   - Top level Classes or interface can not be declared as private because
     1. private means “only visible within the enclosing class”.
     2. protected means “only visible within the enclosing class and any subclasses”

   Hence these modifiers in terms of application to classes, they apply only to nested classes and not on top level classes

3. Protected
   **protected**: The protected access modifier is specified using the keyword protected.

   - The methods or data members declared as protected are accessible within same package or sub classes in different package.

4. Public
   **public**: The public access modifier is specified using the keyword public.
   - The public access modifier has the widest scope among all other access modifiers.
   - Classes, methods or data members which are declared as public are accessible from every where in the program. There is no restriction on the scope of a public data members.

![image](https://media.geeksforgeeks.org/wp-content/cdn-uploads/Access-Modifiers-in-Java.png)

### Q9 How garbage collector knows that the object is not in use and needs to be removed?

Garbage collector reclaims objects that are no longer being used, clears their memory, and keeps the memory available for future allocations. This is done via bookkeeping the references to the objects. Any unreferenced object is a garbage and will be collected.

### Q10 Can Java thread object invoke start method twice?

```java
public class MyExmpCode extends Thread{

	public void run(){
		System.out.println("Run");
	}

	public static void main(String a[]){
		Thread t1 = new Thread(new MyExmpCode());
		t1.start();
		t1.start();
	}
}
```

> **Answer:**
> No, it throws IllegalThreadStateException

### Q11 Give the list of Java Object class methods.

> **Answer:**
> clone( ) - Creates and returns a copy of this object.
> equals( ) - Indicates whether some other object is "equal to" this one.
> finalize( ) - Called by the garbage collector on an object when garbage collection
> determines that there are no more references to the object.
> getClass( ) - Returns the runtime class of an object.
> hashCode( ) - Returns a hash code value for the object.
> notify( ) - Wakes up a single thread that is waiting on this object's monitor.
> notifyAll( ) - Wakes up all threads that are waiting on this object's monitor.
> toString( ) - Returns a string representation of the object.
> wait( ) - Causes current thread to wait until another thread invokes the notify() method
> or the notifyAll() method for this object.

```java
public final native Class<?> getClass()//native方法，用于返回当前运行时对象的Class对象，使用了
final关键字修饰，故不允许子类重写。
public native int hashCode() //native方法，用于返回对象的哈希码，主要使用在哈希表中，比如JDK中的
HashMap。
public boolean equals(Object obj)//用于比较2个对象的内存地址是否相等，String类对该方法进行了重写用户
比较字符串的值是否相等。
protected native Object clone() throws CloneNotSupportedException//naitive方法，用于创建并返回
当前对象的一份拷贝。一般情况下，对于任何对象 x，表达式 x.clone() != x 为true，x.clone().getClass()
== x.getClass() 为true。Object本身没有实现Cloneable接口，所以不重写clone方法并且进行调用的话会发生
CloneNotSupportedException异常。
public String toString()//返回类的名字@实例的哈希码的16进制的字符串。建议Object所有的子类都重写这个方
法。
public final native void notify()//native方法，并且不能重写。唤醒一个在此对象监视器上等待的线程(监视
器相当于就是锁的概念)。如果有多个线程在等待只会任意唤醒一个。
public final native void notifyAll()//native方法，并且不能重写。跟notify一样，唯一的区别就是会唤醒
在此对象监视器上等待的所有线程，而不是一个线程。
public final native void wait(long timeout) throws InterruptedException//native方法，并且不能
重写。暂停线程的执行。注意：sleep方法没有释放锁，而wait方法释放了锁 。timeout是等待时间。
public final void wait(long timeout, int nanos) throws InterruptedException//多了nanos参数，
这个参数表示额外时间（以毫微秒为单位，范围是 0-999999）。 所以超时的时间还需要加上nanos毫秒。
public final void wait() throws InterruptedException//跟之前的2个wait方法一样，只不过该方法一直等
待，没有超时时间这个概念
protected void finalize() throws Throwable { }//实例被垃圾回收器回收的时候触发的操作
```

### Q12 Can we override static method?

> **Answer:**
> We cannot override static methods. Static methods are belogs to class, not belongs
> to object. Inheritance will not be applicable for class members

### Q13 Can you list serialization methods?

> **Answer:**
> Serialization interface does not have any methods. It is a marker interface.
> It just tells that your class can be serializable.

### Q14 What is the difference between super() and this()?

> Answer:
> super() is used to call super class constructor, whereas this() used to call
> constructors in the same class, means to call parameterized constructors.

### Q15 How to prevent a method from being overridden?

> **Answer:**
> By specifying final keyword to the method you can avoid overriding
> in a subcalss. Similarlly one can use final at class level to
> prevent creating subclasses.

### Q16 Can we create abstract classes without any abstract methods?

> **Answer:**
> Yes, we can create abstract classes without any abstract methods.

### Q17 How to destroy the session in servlets?

> **Answer:**
> By calling invalidate() method on session object, we can destory the session.

### Q18 Explain Final keyword in java?

> Final keyword in java is used to restrict usage of variable, class and method.

> 1. **Variable**: Value of Final variable is constant, you can not change it.
> 2. **Method**: you can’t override a Final method.
>    A Java method with the final keyword is called a final method and it can not be overridden in the subclass. You should make a method final in Java if you think it’s complete and its behavior should remain constant in sub-classes. In general, final methods are faster than non-final methods because they are not required to be resolved during run-time and they are bonded at compile time.
> 3. **Class**: you can’t inherit from Final class.
>    The final class is complete in nature and can not be sub-classed or inherited. Several classes in Java are final e.g. String, Integer, and other wrapper classes.

### Q19 When is the super keyword used?

> super keyword is used to refer:

- immediate parent class constructor,
- immediate parent class variable,
- immediate parent class method.
  refer [this](https://www.geeksforgeeks.org/commonly-asked-java-programming-interview-questions-set-1/) for details.

### Q20 What is the difference between StringBuffer and String?

> String is an Immutable class, i.e. you can not modify its content once created. While StringBuffer is a mutable class, means you can change its content later. Whenever we alter content of String object, it creates a new string and refer to that,it does not modify the existing one. This is the reason that the performance with StringBuffer is better than with String.
> Refer [this](https://www.geeksforgeeks.org/string-vs-stringbuilder-vs-stringbuffer-in-java/) for details.
> **When to use which one :**

- If a string is going to remain constant throughout the program, then use String class object because a String object is immutable.
- If a string can change (example: lots of logic and operations in the construction of the string) and will only be accessed from a single thread, using a StringBuilder is good enough.
- If a string can change, and will be accessed from multiple threads, use a StringBuffer because StringBuffer is synchronous so you have thread-safety.

### Q21 Why multiple inheritance is not supported in java?

> Java supports multiple inheritance but not through classes, it supports only through its interfaces. The reason for not supporting multiple inheritance is to avoid the conflict and complexity arises due to it and keep Java a Simple Object Oriented Language. If we recall this in C++, there is a special case of multiple inheritance (diamond problem) where you have a multiple inheritance with two classes which have methods in conflicts. So, Java developers decided to avoid such conflicts and didn’t allow multiple inheritance through classes at all.

### Q22 What is the difference between ‘throw’ and ‘throws’ in Java Exception Handling?

> - throw keyword is used to throw Exception from any method or static block whereas throws is used to indicate that which Exception can possibly be thrown by this method

- If any method throws checked Exception, then caller can either handle this exception(using try catch block )or can re throw it by declaring another ‘throws’ clause in method declaration.
- throw clause can be used in any part of code where you feel a specific exception needs to be thrown to the calling method
  ![image](https://iknow-pic.cdn.bcebos.com/94cad1c8a786c917168f224fc43d70cf3bc75733?x-bce-process=image/resize,m_lfit,w_600,h_800,limit_1)
  ![image](https://iknow-pic.cdn.bcebos.com/bd315c6034a85edfc6478e5544540923dc5475f8?x-bce-process=image/resize,m_lfit,w_600,h_800,limit_1)

**Another Answer:**
Though they are similar in terms that both are used in Exception handling, they are different on how and where they are used in code. throws keyword is used in method signature to declare which checked exception method can throw, you can also declare unchecked exception, but that is not mandatory by the compiler.

This signifies a lot of things like method is not going to handle Exception instead it's throwing it, if method throws checked Exception then the caller should provide compile-time exception handling etc.

On the other hand, throw keyword is actually used to throw any Exception. Syntactically you can throw any Throwable (i.e. Throwable or any class derived from Throwable) , throw keyword transfers control of execution to the caller so it can be used in place of return keyword. Most common example of using throw in place of return is throwing UnSupportedOperationException from an empty method as shown below :

```java
private static void show() { throw new UnsupportedOperationException("Not yet implemented"); }

```

### Q23 What is finalize() method?

> Unlike c++ , we don’t need to destroy objects explicitly in Java. ‘Garbage Collector‘ does that automatically for us. Garbage Collector checks if no references to an object exist, that object is assumed to be no longer required, and the memory occupied by the object can be freed. Sometimes an object can hold non-java resources such as file handle or database connection, then you want to make sure these resources are also released before object is destroyed. To perform such operation Java provide protected void finalize() in object class. You can override this method in your class and do the required tasks. Right before an object is freed, the java run time calls the finalize() method on that object. Refer this for more details.

### Q24 Difference in Set and List interface?

> Set and List both are child interface of Collection interface. There are following two main differences between them

- List can hold duplicate values but Set doesn’t allow this.
- In List interface data is present in the order you inserted but in the case of Set insertion order is not preserved.

### Q25 What will happen if you put System.exit(0) on try or catch block? Will finally block execute?

> By Calling System.exit(0) in try or catch block, we can skip the finally block. System.exit(int) method can throw a SecurityException. If Sysytem.exit(0) exits the JVM without throwing that exception then finally block will not execute. But, if System.exit(0) does throw security exception then finally block will be executed.

### Q26 Overriding vs. Overloading

![image](https://www.programcreek.com/wp-content/uploads/2009/02/overloading-vs-overriding.png?ezimgfmt=ng:webp/ngcb7)

1. Defination:
   **Overloading** occurs when two or more methods in one class have the same method name but different parameters.
   **Overriding** means having two methods with the same method name and parameters (i.e., method signature). One of the methods is in the parent class and the other is in the child class. Overriding allows a child class to provide a specific implementation of a method that is already provided its parent class.

2. Overridding vs. Overloading
   - The real object type in the run-time, not the reference variable's type, determines which overridden method is used at runtime. In contrast, reference type determines which overloaded method will be used at compile time.
   * Polymorphism applies to overriding, not to overloading.
   * Overriding is a run-time concept while overloading is a compile-time concept.

### Q27 String vs StringBuffer vs StringBuilder

![image](https://cdn.journaldev.com/wp-content/uploads/2010/12/StringBuffer-vs-StringBuilder-1.png)

1. String in Java

- String is immutable in Java. So it’s suitable to use in a multi-threaded environment. We can share it across functions because there is no concern of data inconsistency.

* When we create a String using double quotes, JVM first looks for the String with the same value in the string pool. If found, it returns the reference of the string object from the pool. Otherwise, it creates the String object in the String pool and returns the reference. JVM saves a lot of memory by using the same String in different threads.
* If the new operator is used to create a string, it gets created in the heap memory.
* String overrides equals() and hashCode() methods. Two Strings are equal only if they have the same character sequence. The equals() method is case sensitive. If you are looking for case insensitive checks, you should use equalsIgnoreCase() method.
* String is a final class. All the fields as final except “private int hash”. This field contains the hashCode() function value. The hashcode value is calculated only when the hashCode() method is called for the first time and then cached in this field. Furthermore, the hash is generated using the final fields of String class with some calculations. So every time the hashCode() method is called, it will result in the same output. For the caller, it seems like calculations are happening every time but internally it’s cached in the hash field.

**String vs StringBuffer**
Since String is immutable in Java, whenever we do String manipulation like concatenation, substring, etc. it generates a new String and discards the older String for garbage collection.
These are heavy operations and generate a lot of garbage in heap. So Java has provided StringBuffer and StringBuilder classes that should be used for String manipulation.
StringBuffer and StringBuilder are mutable objects in Java. They provide append(), insert(), delete(), and substring() methods for String manipulation.
**StringBuffer vs StringBuilder**
StringBuffer was the only choice for String manipulation until Java 1.4. But, it has one disadvantage that all of its public methods are synchronized. StringBuffer provides Thread safety but at a performance cost.
In most of the scenarios, we don’t use String in a multithreaded environment. So Java 1.5 introduced a new class StringBuilder.
If you are in a single-threaded environment or don’t care about thread safety, you should use StringBuilder. Otherwise, use StringBuffer for thread-safe operations.

### Q27 Autoboxing and Unautoboxing in Java

Converting a primitive data type into an object of the corresponding wrapper class is called **autoboxing**. For example, converting int to Integer or converting long to Long object.
Converting an object of a wrapper type to its corresponding primitive data type is called **unboxing**.

### Q28 Exception Handling in Java

![image](https://img-blog.csdn.net/20160326233035366)
In Java Exception feature is implemented by using class like Throwable, Exception, RuntimeException and keywords like throw, throws, try, catch and finally. All Exception are derived from Throwable class.
Throwable further divides errors in two category one is java.lang.Exception and other is java.lang.Error. java.lang.Error deals with system errors like java.lang.StackOverFlowError or Java.lang.OutOfMemoryError while Exception is mostly used to deal with programming mistakes, non availability of requested resource etc.

| ArithmeticException                                                                             | int a=0;<br>int b= 3/a;                                      |
| ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| ClassCastException：                                                                            | Object x = new Integer(0);<br>System.out.println((String)x); |
| IndexOutOfBoundsException<br>ArrayIndexOutOfBoundsException <br>StringIndexOutOfBoundsException | int [] numbers = { 1, 2, 3 };<br><br>int sum = numbers[3];   |
| IllegalArgumentException<br>NumberFormatException                                               | int a = Interger.parseInt("test");                           |
| NullPointerExceptionextends                                                                     | 继承自 RuntimeException，所以它是个 unchecked exception      |

### Q29 What is the difference between Checked and Unchecked Exception in Java?

Main difference between Checked and Unchecked Exception lies in there handling. Checked Exception requires to be handled at compile time using try, catch and finally keywords or else compiler will flag error. This is not a requirement for Unchecked Exceptions. Also all exceptions derived from java.lang.Exception classes are checked exception, exception those which extends RuntimeException, these are known as unchecked exception in Java.

### Q30 获取用键盘输入常用的的两种方法

**方法 1：通过 Scanner**

```java
Scanner input = new Scanner(System.in);
String s = input.nextLine();
input.close();
```

**方法 2：通过 BufferedReader**

```java
BufferedReader input = new BufferedReader(new InputStreamReader(System.in));
String s = input.readLine();
```

### Q31 Difference between abstract class and interface

Abstract class and interface both are used to achieve abstraction where we can declare the abstract methods. Abstract class and interface both can't be instantiated.
But there are many differences between abstract class and interface that are given below.
| Abstract class | Interface |
| ---- | ---- |
| **1.** Abstract class can have abstract and non-abstract methods. | Interface can have only abstract methods. Since Java 8, it can have default and static methods also. |
| **2.** Abstract class doesn't support multiple inheritance.| Interface supports multiple inheritance. |
| **3.** Abstract class can have final, non-final, static and non-static variables.| Interface has only static and final variables. |
| **4.** Abstract class can provide the implementation of interface.| Interface can't provide the implementation of abstract class. |
| **5.** The abstract keyword is used to declare abstract class. | The interface keyword is used to declare interface. |
| **6.** An abstract class can extend another Java class and implement multiple Java interfaces. | An interface can extend another Java interface only. |
| **7.** An abstract class can be extended using keyword "extends". | An interface can be implemented using keyword "implements". |
| **8.** A Java abstract class can have class members like private, protected, etc. | Members of a Java interface are public by default. |

### Q32 What is Inheritance in Java?

Inheritance is an Object oriented feature which allows a class to inherit behavior and data from other class. For example, a class Car can extend basic feature of Vehicle class by using Inheritance. One of the most intuitive examples of Inheritance in the real world is Father-Son relationship, where Son inherit Father's property.

### Q32 What are different types of Inheritance supported by Java?

Java supports single Inheritance, multi-level inheritance and at some extent multiple inheritances because Java allows a class to only extend another class, but an interface in Java can extend multiple inheritances.

### Q32 Why multiple Inheritance is not supported by Java?

Java is introduced after C++ and Java designer didn't want to take some C++ feature which is confusing and not essential. They think multiple inheritances is one of them which doesn't justify complexity and confusion it introduces.

### Q33 What is the difference between Inheritance and Abstraction?

- In Interfaces, all the methods will not have method implementation.
- The class which is implementing the interface should implement all the methods in that particular interface.
- Abstract classes can have abstract methods as well as normal concrete methods. Abstract methods don’t have an implementation.
- The class which is extending the abstract class should have the implementation for all the abstract methods in the abstract class.
- If the subclass doesn’t have enough information to implement the abstract methods, then the subclass should be declared as an abstract class.

### Q34 Can we override static method in Java?

No, you cannot override a static method in Java because it's resolved at compile time. In order for overriding to work, a method should be virtual and resolved at runtime because objects are only available at runtime.

### Q35 The four principles of object-oriented programming are encapsulation, abstraction, inheritance, and polymorphism

**Encapsulation:** Encapsulation is the mechanism of binding the data together and hiding it from the outside world. Encapsulation is achieved when each object keeps its state private so that other objects don’t have direct access to its state. Instead, they can access this state only through a set of public functions.

**Abstraction:** Abstraction can be thought of as the natural extension of encapsulation. It means hiding all but the relevant data about an object in order to reduce the complexity of the system. In a large system, objects talk to each other, which makes it difficult to maintain a large code base; abstraction helps by hiding internal implementation details of objects and only revealing operations that are relevant to other objects.

**Inheritance:** The idea behind inheritance in Java is that you can create new classes that are built upon existing classes. When you inherit from an existing class, you can reuse methods and fields of the parent class. Moreover, you can add new methods and fields in your current class also. The extends keyword indicates that you are making a new class that derives from an existing class. The meaning of "extends" is to increase the functionality.

**Polymorphism:** Polymorphism is the ability of an object to take on many forms. The most common use of polymorphism in OOP occurs when a parent class reference is used to refer to a child class object.
Any Java object that can pass more than one IS-A test is considered to be polymorphic. In Java, all Java objects are polymorphic since any object will pass the IS-A test for their own type and for the class Object.

It is important to know that the only possible way to access an object is through a reference variable. A reference variable can be of only one type. Once declared, the type of a reference variable cannot be changed.

The reference variable can be reassigned to other objects provided that it is not declared final. The type of the reference variable would determine the methods that it can invoke on the object.

A reference variable can refer to any object of its declared type or any subtype of its declared type. A reference variable can be declared as a class or interface type.

### Q36 Multithreading and Life Cycle of a thread

A multi-threaded program contains two or more parts that can run concurrently and each part can handle a different task at the same time making optimal use of the available resources specially when your computer has multiple CPUs.
**Life Cycle of a Thread**
![image](https://www.tutorialspoint.com/java/images/Thread_Life_Cycle.jpg)

- **New** − A new thread begins its life cycle in the new state. It remains in this state until the program starts the thread. It is also referred to as a born thread.

- **Runnable** − After a newly born thread is started, the thread becomes runnable. A thread in this state is considered to be executing its task.

- **Waiting** − Sometimes, a thread transitions to the waiting state while the thread waits for another thread to perform a task. A thread transitions back to the runnable state only when another thread signals the waiting thread to continue executing.

- **Timed Waiting** − A runnable thread can enter the timed waiting state for a specified interval of time. A thread in this state transitions back to the runnable state when that time interval expires or when the event it is waiting for occurs.

- **Terminated** (Dead) − A runnable thread enters the terminated state when it completes its task or otherwise terminates.

**Create a Thread by Implementing a Runnable Interface**
**Create a Thread by Extending a Thread Class**
初始化线程的 4 种方式：

1. 继承 Thread
2. 实现 Runnable 接口
3. 实现 Callable 接口 + FutureTask （可以拿到返回结果，可以处理异常）
4. 线程池

```java
Executors.newFiexedThreadPool(3);
//或者
new ThreadPoolExecutor(corePoolSize, maximumPoolSize, keepAliveTime, TimeUnit unit, workQueue, threadFactory, handler);
```

### Q37 What id Thread Synchronization?

When we start two or more threads within a program, there may be a situation when multiple threads try to access the same resource and finally they can produce unforeseen result due to concurrency issues.
Java programming language provides a very handy way of creating threads and synchronizing their task by using synchronized blocks.

### Q38 Handling thread deadlock?

Deadlock describes a situation where two or more threads are blocked forever, waiting for each other. Deadlock occurs when multiple threads need the same locks but obtain them in different order.

In order to avoid deadlock, you have to acquire a lock in the fixed order.

### Q39 What is Thread Safty?

Thread safe means that a method or class instance can be used by multiple threads at the same time without any problem.

### Q40 What is Concurrency?

In simple words, concurrency is the ability to run several programs or several parts of a program in parallel.

### Difference between Runnable vs Thread in Java

#### 1. Create Thread using Runnable Interface vs Thread class

##### 1.1. Runnable interface

```java
public class DemoRunnable implements Runnable {
    public void run() {
        //Code
    }
}

//start new thread with a "new Thread(new demoRunnable()).start()" call
```

##### 1.2. Thread class

```java
public class DemoThread extends Thread {
    public DemoThread() {
        super("DemoThread");
    }
    public void run() {
        //Code
    }
}
//start new thread with a "new demoThread().start()" call
```

#### 2. Difference between Runnable vs Thread

1. Implementing Runnable is the preferred way to do it. Here, you’re not really specializing or modifying the thread’s behavior. You’re just giving the thread something to run. That means composition is the better way to go.

2. Java only supports single inheritance, so you can only extend one class.

3. Instantiating an interface gives a cleaner separation between your code and the implementation of threads.

4. Implementing Runnable makes your class more flexible. If you extend Thread then the action you’re doing is always going to be in a thread. However, if you implement Runnable it doesn’t have to be. You can run it in a thread, or pass it to some kind of executor service, or just pass it around as a task within a single threaded application.

5. when there are multiple threads then, memory usage would be more in case of extends Thread. Because, each of your threads contains unique object associated with it. Where as, memory usage would be less in case of implements Runnable. Because, many threads can share the same runnable instance.

我们先来看 Thread 和 Runnable，最直接的区别是，Thread 是一个类，需要继承，而 Runnable 是一个接口，需要实现。我们知道，Java 中，是单继承多实现的，即一个类，通过 extends 只能继承一个类，而通过 implements 关键字，可以实现多个接口。所以，就这两种方法而言，更推荐使用实现 Runnable 接口的方式。这样，extends 可以留给更需要的人。

Runnable 还有一个优势，我们可以通过分析 Thread 的源码发现。Thead 类中，有一个属性，类型是 Runnable，名称是 target。也就是说，当我们调用 start 方法启动线程后，事实上在运行时，执行的是 target 的 run 方法。注意我们在使用 Runnable 时做的事情，是先 new 了一个 Runnable 类的实例，再将其包装成一个 Thread 的实例，再执行 start 方法，就好像是我们把 Runnable 和 Thread 作了一定程度的解耦，换句话说，我们把线程的创建和具体的业务做了解耦。这样的好处是什么？一是代码和数据独立，二是多线程可以共享同一个资源。

代码和数据独立很好理解，那么，多线程共享资源是什么意思？看如下：
![image](https://pics1.baidu.com/feed/b17eca8065380cd77f77a1e09c6aa53159828101.png?token=5194a4a9d98e80cdd102e73f403518f3&s=1AAA7023CD226D224C5540DA030080B1)
我们看到，创建了两个线程，但是它们使用了同一个 Runnable 实例。也就意味着，如果 Runnable 实例中包含一个类变量，比如 count，那么，两个线程对 count 的操作是相互影响的，也就是说，count 这个变量是两个线程共享的，Runnable 实例是两个线程共享的。

### Q41 What is a thread local variable?

In Java there is a class called ThreadLocal which provides another way of thread-safety apart from synchronization. Usually when we have multiple threads sharing an object we need to synchronize the critical section of the code in order to make it thread safe.
ThreadLocal class provides thread-local variables where each thread that accesses one (via its get or set method) has its own, independently initialized copy of the variable. Since each and every threadhas its own copy of the object so explicit synchronization is not needed to provide thread safety.

### Q42 What is the difference between sleep and wait?

- The very first difference is that sleep is defined as a static method in Thread class and operates on the currently executing thread. Whereas wait() method is in Object class and operates on the thread which is currently holding the lock on the object on which the wait method is called.
- Since wait method is supposed to release the lock on an object so it has to be called from a synchronized context (with in a synchronized method or synchronized block). If not called from a synchronized context will result in a IllegalMonitorStateException being thrown. With sleep method there is no such mandatory condition it doesn't need to be called from a synchronized context.
- Wait method will release the lock it holds on an object before going to waiting state which gives another thread a chance to enter the synchronized block. Sleep method if called from a synchronized block or method will not release the lock so another won't get a chance to enter the synchronized block.

### Q43 What is the difference between notify() and notifyAll()?

- **Notify** method wakes up a single thread that is waiting to acquire a lock on the object. If more than one threads are waiting on this object, one of them is chosen to be awakened.

- **NotifyAll** method wakes up all the threads that called wait on the same object. Note that only one of these threads will get a lock to the object.

### Q44 What are the different thread states?

**New** - When a thread is created either by extending Thread class or implementing Runnable interface it is in "New State".
**Runnable** - When we call start() method on the thread object that causes the thread to begin execution and it's the Java Virtual Machine that calls the run method of the thread.
**Blocked** - When a resource is shared among various threads then a thread may go into blocked state as the resource may be used by another thread.
**Waiting** - A thread that is waiting indefinitely for another thread to perform a particular action is in the waiting state.
**Timed_Waiting** - A thread that is waiting for another thread to perform an action for up to a specified waiting time is in timed_waiting state.

### Q45 What is the difference between thread and process?

- A process has a self-contained execution environment, Threads exist within a process - every process has at least one.
- Process are heavyweight tasks whereas threads are referred as lightweight processes as creating a new thread requires fewer resources than creating a new process.
- Each Process has its own separate address spaces, threads with in the same process share the process' resources, including memory and open files. This means that it's very easy to share data amongst threads, but it's also easy for the threads to bump on each other, which can lead to unpredictable scenarios.
- Inter process communication is expensive whereas inter thread communication is inexpensive and in Java can be achieved easily using wait and notify.
- Context switching from one process to another is expensive; context switching between threads is generally less expensive than in processes.
- Threads are easier to create than processes as separate address space is not required for a thread.-

### Q46 How do we create thread in Java?

In Java there are two ways to create thread.

- By implementing the Runnable interface.
- By extending the Thread class.

### Q47 Difference between Vector and ArrayList?

- All the methods of Vector is synchronized. But, the methods of ArrayList is not synchronized.

- By default, Vector doubles the size of its array when it is re-sized internally. But, ArrayList increases by half of its size when it is re-sized.

### Q48 Difference between HashMap and HashTable?

- Hashtable is synchronized, whereas HashMap is not.

- Hashtable does not allow null keys or values. HashMap allows one null key and any number of null values.

- The third significant difference between HashMap vs Hashtable is that Iterator in the HashMap is a fail-fast iterator while the enumerator for the Hashtable is not.

### Q49 Difference between Set and List?

- Set is unordered collection where List is ordered collection based on zero based index.
- List allow duplicate elements but Set does not allow duplicates.
- List does not prevent inserting null elements (as many you like), but Set will allow only one null element.

### Q50 How to design a good key for hashmap?

HashMap is well known class and all of us know that. So, I will leave this part by saying that it is used to store key-value pairs and allows to perform many operations on such collection of pairs.

TreeMap is special form of HashMap. It maintains the ordering of keys which is missing in HashMap class. This ordering is by default “natural ordering”. The default ordering can be override by providing an instance of Comparator class, whose compare method will be used to maintain ordering of keys.

### Q51 How hashmap works?

Answer to this question is very large and you should read it my post: How HashMap works? For now, lets remember that HashMap works on principle of Hashing. A map by definition is : “An object that maps keys to values”. To store such structure, it uses an inner class Entry:

```java
static class Entry implements Map.Entry
{
final K key;
V value;
Entry next;
final int hash;
...//More code goes here
}
```

Here key and value variables are used to store key-value pairs. Whole entry object is stored in an array.

```java
/**
* The table, re-sized as necessary. Length MUST Always be a power of two.
*/
transient Entry[] table;
```

The index of array is calculated on basis on hashcode of Key object. Read more of linked topic.

### What is REST?

REST, or Representational State Transfer, is an architectural design that defines a set of rules for creating web services that interact between systems. Web services that follow this architecture are termed, ‘RESTful web services’.

At a very high level, the RESTful system consists of two major components:

A server that hosts the resources

A client that connects to the server to fetch the resources

REST uses HTTP (Hypertext Transfer Protocol) or HTTPS (Hypertext Transfer Protocol Secure) to exchange data between client and server using HTTP methods – GET, POST, UPDATE, DELETE, HEAD, PATCH, etc.

Benefits of using REST #
By following the principles of REST, we can benefit from the loose coupling between the server and the client, reliability, scalability, and better performance of the application. Few of the benefits of REST are listed below:

Simplicity – REST web services are easy and simple to develop compared to SOAP web services

Light-weight – REST advocates simple communication with the server over HTTP that supports plain XML, JSON formats in comparison to SOAP which supports only XML

Architecture is similar to Web --the architecture of REST is very similar to how the web is designed. So, developers who understand the web can easily understand and develop RESTful web services

Scalability – the REST architecture advocates refraining from the conversational state that allows us to easily add multiple instances of the components or application behind load balancers
