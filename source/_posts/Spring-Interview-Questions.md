---
title: Spring Interview Questions
date: 2020-07-04 15:50:09
tags:
    - Spring
---

## Q1 Differences Between Spring and Spring Boot
**Spring**: 
The Spring Framework is one of the most popular frameworks which helps application development in Java. It maintained a various way of object or beans relationship. It is actually very much useful for dependency injection (DI) or Inversion of Control (IOC), which wonderfully helped us to develop loosely coupled applications, which automatically helped proper unit testing of any Java application.
Aspect-Oriented Program (AOP) mainly used for any aspect like security or logging integration with any Java application, special features of it, and this feature can be called before or after a method call after a method return or exception arises in the application. Spring can be easily integrated with any ORM tool. Spring test for testing purpose and expression language are using for view presentation.


**Spring Boot**: 
Spring Boot is a module of Spring Framework. Spring boot is actually based on all the default features of spring. Core Spring and MVC can able to handle entire require features of any Java application. As per complexity and configuration, spring boot can help us lot to reduce spring configuration related complexity. It is better to use if we want to develop a simple Spring-based application or RESTful services.

![image](https://cdn.educba.com/academy/wp-content/uploads/2018/09/Spring-Vs-Spring-Boot.jpg)

> Key Differences Between Spring vs Spring Boot

1. Spring is mainly concentrated on its core features and MVC features where a developer needs to configure manually and define which feature needs to be used by the application as per requirement. Whereas Spring Boot is automatically loaded all the features of spring core and MVC automatically. Developer no need to define any specific configuration manually.
2. Spring core has multiple modules which can be used for different purpose and resolving some common utilities as per java application requirements. Modules like Spring JDBC, MVC, AOP, ORM etc are very much useful for any aspect as per project requirements. All those utilities can be properly configured and utilized as per system or project requirements. Whereas Spring Boot can utilize all those requirements easily just define the application as @SpringBootConfiguration, that annotation enough to manage for loading entire spring configuration or all the modules features based on the jar files or dependency mentioned for that specific spring boot project.
3. Transaction management is one of most critical job in any Spring application, developer has to define proper transactional management key for every hibernate session or DB connection (in case of Spring JDBC), spring specific transactional class needs to be defined in application-specific configuration file for using those in entire application which can manage the transaction properly. Whereas Spring Boot automatically managed entire transactional data without mentioning any specific configuration manually, the entire thing can be handled automatically. A transaction can be defined in every session or connection opening and closing. A transaction can be commit or rollback based on the entire task of that specific session completion status.
4. Integration with any ORM tool is very critical for any kind of spring application, needs to define their data source properly in the configuration file manually by the developer, there have changes need to be done for any ORM tool exchange. In case of spring boot again it can be easy to auto-configured, no need of manual intervention, only define one database property file is enough for entire set up.
5. Spring core or Spring MVC structure developer can easily maintain on loading only require feature based on project requirement. Whereas the case of spring boot, all the features defined in dependency or jar files will be automatically loaded, a developer has no control of not deploying any specific feature based on project requirement.

> Conclusion – Spring vs Spring Boot

Spring vs Spring Boot both are a very much popular framework for Java/J2EE application at any time. Normally developer is going to choose which framework will be better to use based on the application requirement or functionality. Suppose application have some possibility of using verities Spring modules in any circumstances on future integration, in that case, Spring boot will be always a better option to use because just adding require dependency or jar file enough to use that specific module integration with your existing application. But if an application doesn’t have that kind of future prospect, or plan to only make a pure web application, in that case, Spring MVC will be a good approach, as a developer have a lot of control on the features enable or disable.

## Q2 What Spring Boot Starters Are Available out There?
Dependency management is a crucial facet of any project. When a project is complex enough, managing dependencies may turn into a nightmare, as there will be too many artifacts involved
This is where Spring Boot starters come in handy. Each starter plays a role as a one-stop shop for all the Spring technologies we need. Other required dependencies are then transitively pulled in and managed in a consistent way.

All starters are under the org.springframework.boot group, and their names start with spring-boot-starter-. **This naming pattern makes it easy to find starters, especially when working with IDEs that support searching dependencies by name.**
- **spring-boot-starter**: core starter, including auto-configuration support, logging, and YAML
- **spring-boot-starter-aop**: starter for aspect-oriented programming with Spring AOP and AspectJ
- **spring-boot-starter-data-jpa**: starter for using Spring Data JPA with Hibernate
- **spring-boot-starter-jdbc**: starter for using JDBC with the HikariCP connection pool
- **spring-boot-starter-security**: starter for using Spring Security
- **spring-boot-starter-test**: starter for testing Spring Boot applications
- **spring-boot-starter-web**: starter for building web, including RESTful, applications using Spring MVC


## What is Spring IOC Container?
![image](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/05/ioc-2.png)At the core of the Spring Framework, lies the Spring container. The container creates the object, wires them together, configures them and manages their complete life cycle. The Spring container makes use of Dependency Injection to manage the components that make up an application. The container receives instructions for which objects to instantiate, configure, and assemble by reading the configuration metadata provided. This metadata can be provided either by XML, Java annotations or Java code.
## Q3 What do you mean by Dependency Injection?
In Dependency Injection, you do not have to create your objects but have to describe how they should be created. You don’t connect your components and services together in the code directly, but describe which services are needed by which components in the configuration file. The IoC container will wire them up together.
## Q4 In how many ways can Dependency Injection be done?
In general, dependency injection can be done in three ways, namely :
* **Constructor Injection**
* **Setter Injection**
* Interface Injection

In Spring Framework, only constructor and setter injections are used.

## Q5 How many types of IOC containers are there in spring?

* **BeanFactory**: BeanFactory is like a factory class that contains a collection of beans. It instantiates the bean whenever asked for by clients.
* **ApplicationContext**: The ApplicationContext interface is built on top of the BeanFactory interface. It provides some extra functionality on top BeanFactory.

## Q6 Differentiate between BeanFactory and ApplicationContext.
BeanFactory vs ApplicationContext

|  **BeanFactory**   | **ApplicationContext**  |
|  ----  | ----  |
| It is an interface defined in org.springframework.beans.factory.**BeanFactory**  | It is an interface defined in org.springframework.context.**ApplicationContext** |
| It uses Lazy initialization  | It uses Eager/ Aggressive initialization |
| It explicitly provides a resource object using the syntax  | It creates and manages resource objects on its own |
| It doesn’t supports internationalization  | It supports internationalization  |
| It doesn’t supports annotation based dependency   | It supports annotation based dependency   |

## Q7 Explain Spring Beans?
* They are the objects that form the backbone of the user’s application.
* Beans are managed by the Spring IoC container.
* They are instantiated, configured, wired and managed by a Spring IoC container
* Beans are created with the configuration metadata that the users supply to the container.
![image](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/05/bean.png)

## Q8 How configuration metadata is provided to the Spring container?
Configuration metadata can be provided to Spring container in following ways:
* **XML-Based configuration**: In Spring Framework, the dependencies and the services needed by beans are specified in configuration files which are in XML format. These configuration files usually contain a lot of bean definitions and application specific configuration options. They generally start with a bean tag. For example:
```shell script
<bean id="studentbean" class="org.edureka.firstSpring.StudentBean">
 <property name="name" value="Edureka"></property>
</bean>
```
* **Annotation-Based configuration**: Instead of using XML to describe a bean wiring, you can configure the bean into the component class itself by using annotations on the relevant class, method, or field declaration. By default, annotation wiring is not turned on in the Spring container. So, you need to enable it in your Spring configuration file before using it. For example:
```shell script
<beans>
<context:annotation-config/>
<!-- bean definitions go here -->
</beans>
```
* **Java-based configuration**: The key features in Spring Framework’s new Java-configuration support are @Configuration annotated classes and @Bean annotated methods. 
 > 1. @Bean annotation plays the same role as the <bean/> element. 
  2. @Configuration classes allows to define inter-bean dependencies by simply calling other @Bean methods in the same class. 
  
 ```java
 @Configuration
public class StudentConfig 
{ 
@Bean
public StudentBean myStudent() 
{ return new StudentBean(); }
}
```

## Q9 What are Beans in Spring?

When a class is annotated or decorated using the @Component, such a class is called a Bean in Spring. Beans are maintained by Application Context.

## Q10 What Is Dependency Injection?
Dependency Injection, an aspect of Inversion of Control (IoC), is a general concept stating that you do not create your objects manually but instead describe how they should be created. An IoC container will instantiate required classes if needed.

## Q11 What Are the Benefits of Using Spring？
Spring targets to make Jakarta EE development easier. Here are the advantages of using it:

- **Lightweight:** there is a slight overhead of using the framework in development
- **Inversion of Control (IoC):** Spring container takes care of wiring dependencies of various objects, instead of creating or looking for dependent objects
- **Aspect Oriented Programming (AOP):** Spring supports AOP to separate business logic from system services
- **IoC container:** it manages Spring Bean life cycle and project specific configurations
- **MVC framework:** that is used to create web applications or RESTful web services, capable of returning XML/JSON responses
- **Transaction management:** reduces the amount of boiler-plate code in JDBC operations, file uploading, etc., either by using Java annotations or by Spring Bean XML configuration file
- **Exception Handling:** Spring provides a convenient API for translating technology-specific exceptions into unchecked exceptions

## Q12 What Spring Sub-Projects Do You Know? Describe Them Briefly.
— **Core** – a key module that provides fundamental parts of the framework, like IoC or DI
— **JDBC** – this module enables a JDBC-abstraction layer that removes the need to do JDBC coding for specific vendor databases
— **ORM integration** – provides integration layers for popular object-relational mapping APIs, such as JPA, JDO, and Hibernate
— **Web** – a web-oriented integration module, providing multipart file upload, Servlet listeners, and web-oriented application context functionalities
— **MVC framework **– a web module implementing the Model View Controller design pattern
- **AOP module** – aspect-oriented programming implementation allowing the definition of clean method-interceptors and pointcuts

## Q13 Inversion of Control？
Inversion of Control (IoC) is a design principle， As the name suggests, it is used to invert different kinds of controls in object-oriented design to achieve loose coupling. This include control over the flow of an application, and control over the flow of an object creation or dependent object creation and binding. You don't have to create an object yourself you can let the IOC container do that.

Inversion of Control can be achieved through various mechanisms such as: Strategy design pattern, Service Locator pattern, Factory pattern, and Dependency Injection (DI).

## Q14 How Can We Inject Beans in Spring?
A few different options exist:

- Setter Injection
- Constructor Injection
- Field Injection
The configuration can be done using XML files or annotations.

## Q15 Which Is the Best Way of Injecting Beans and Why?
The recommended approach is to use constructor arguments for mandatory dependencies and setters for optional ones. Constructor injection allows injecting values to immutable fields and makes testing easier.

## Q16 What Is the Difference Between Beanfactory and Applicationcontext?
BeanFactory is an interface representing a container that provides and manages bean instances. The default implementation instantiates beans lazily when getBean() is called.

ApplicationContext is an interface representing a container holding all information, metadata, and beans in the application. It also extends the BeanFactory interface but the default implementation instantiates beans eagerly when the application starts. This behavior can be overridden for individual beans.

## Q17 What Is the Default Bean Scope in Spring Framework?
By default, a Spring Bean is initialized as a singleton.

## Q18 How to Define the Scope of a Bean?
To set Spring Bean's scope, we can use @Scope annotation or “scope” attribute in XML configuration files. There are five supported scopes:

singleton
prototype
request
session
global-session

## Q19 Are Singleton Beans Thread-Safe?
No, singleton beans are not thread-safe, as thread safety is about execution, whereas the singleton is a design pattern focusing on creation. Thread safety depends only on the bean implementation itself.

## Q20 What Is Spring Security?
Spring Security is a separate module of the Spring framework that focuses on providing authentication and authorization methods in Java applications. It also takes care of most of the common security vulnerabilities such as CSRF attacks.

To use Spring Security in web applications, you can get started with a simple annotation: @EnableWebSecurity.

## Q22 What Is Spring Boot?
Spring Boot is a project that provides a pre-configured set of frameworks to reduce boilerplate configuration so that you can have a Spring application up and running with the smallest amount of code.

## Q23 Name Some of the Design Patterns Used in the Spring Framework?
Singleton Pattern: Singleton-scoped beans
Factory Pattern: Bean Factory classes
Prototype Pattern: Prototype-scoped beans
Adapter Pattern: Spring Web and Spring MVC
Proxy Pattern: Spring Aspect Oriented Programming support
Template Method Pattern: JdbcTemplate, HibernateTemplate, etc.
Front Controller: Spring MVC DispatcherServlet
Data Access Object: Spring DAO support
Model View Controller: Spring MVC

## Q24 What Is Aspect-Oriented Programming?
Aspects enable the modularization of cross-cutting concerns such as transaction management that span multiple types and objects by adding extra behavior to already existing code without modifying affected classes.

## Q25 What Are Aspect, Advice, Pointcut, and Joinpoint in Aop?
- **Aspect:** a class that implements cross-cutting concerns, such as transaction management
- **Advice:** the methods that get executed when a specific JoinPoint with matching Pointcut is reached in the application
- **Pointcut:** a set of regular expressions that are matched with JoinPoint to determine whether Advice needs to be executed or not
- **JoinPoint:** a point during the execution of a program, such as the execution of a method or the handling of an exception

## Q29 What are the roles of an IOC (Inversion of Control) Container?

IOC Container does the following things-

**(i)** Find Beans

**(ii)** Identify their dependencies and wire the dependencies

**(iii)** Manage Lifecycle of the Bean (creation, processing, and destruction)

## Q30 What is Application Context?

It is an advanced version of IOC Container. It provides all the functionalities of Bean Factory and also provides things like AOP, Internationalization capabilities, web application context (request, session, etc).

## Q31 Differentiate @Component, @Repository and @Service and @Controller?

Typically a web application is developed in layers like the controller (which is the initial point of client communication), business (where the actual code or logic of the application is written) and DAO (where the database connections and interaction happens). In such an architecture web application, @Component can be used in any of the layers. Whereas, the @Controller is used in the controller/web layer. @Service is used in the business layer and @Repository is used in the DAO layer.

## Q32 List out the different scopes of Bean.

**(i)** Singleton: throughout the spring context only one instance is created.

**(ii)** Prototype: a new bean is created whenever requested.

**(iii)** Request: Every HTTP Request creates a bean.

**(iv)** Session: A bean for every HTTP Session.

## Q33 What Is Spring Webflux?
Spring WebFlux is Spring's reactive-stack web framework, and it's an alternative to Spring MVC.

In order to achieve this reactive model and be highly scalable, the entire stack is non-blocking.

## What Are the Benefits of Using Spring?
Spring targets to make Jakarta EE development easier. Here are the advantages of using it:

- **Lightweight:** there is a slight overhead of using the framework in development
- **Inversion of Control (IoC):** Spring container takes care of wiring dependencies of various objects, instead of creating or looking for dependent objects
- **Aspect Oriented Programming (AOP):** Spring supports AOP to separate business logic from system services
- **IoC container:** it manages Spring Bean life cycle and project specific configurations
- **MVC framework:** that is used to create web applications or RESTful web services, capable of returning XML/JSON responses
- **Transaction management:** reduces the amount of boiler-plate code in JDBC operations, file uploading, etc., either by using Java annotations or by Spring Bean XML configuration file
- **Exception Handling:** Spring provides a convenient API for translating technology-specific exceptions into unchecked exceptions
