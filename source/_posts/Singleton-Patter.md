---
title: Singleton Patter
date: 2020-08-12 22:44:14
tags:
---
This lesson discusses how the Singleton pattern enforces only a single instance of a class to ever get produced and exist throughout an application's lifetime.
### What is it ?
Singleton pattern as the name suggests is used to create one and only instance of a class. There are several examples where only a single instance of a class should exist and the constraint be enforced. Caches, thread pools, registries are examples of objects that should only have a single instance.

Its trivial to new-up an object of a class but how do we ensure that only one object ever gets created? The answer is to make the constructor private of the class we intend to define as singleton. That way, only the members of the class can access the private constructor and no one else.

Formally the Singleton pattern is defined as **ensuring that only a single instance of a class exists and a global point of access to it exists.**
### Class Diagram
The class diagram consists of only a single entity
- Singleton
 ![img](Singleton.png)

 ### Example
 As an example, let's say we want to model the American President's official aircraft called "Airforce One" in our software. There can only be one instance of Airforce One and a singleton class is the best suited representation.

Below is the code for our singleton class
```java
public class AirforceOne {
 
    // The sole instance of the class
    private static AirforceOne onlyInstance;
 
    // Make the constructor private so its only accessible to
    // members of the class.
    private AirforceOne() {
    }
 
    public void fly() {
        System.out.println("Airforce one is flying...");
    }
 
    // Create a static method for object creation
    public static AirforceOne getInstance() {
 
        // Only instantiate the object when needed.
        if (onlyInstance == null) {
            onlyInstance = new AirforceOne();
        }
 
        return onlyInstance;
    }
}
 
public class Client {
 
    public void main() {
        AirforceOne airforceOne = AirforceOne.getInstance();
        airforceOne.fly();
    }
}
```
### Multithreading and Singleton
