---
title: Spring Date JPA
date: 2020-05-20 10:55:14
tags:
---

## Spring Data JPA 简介
Spring Data JPA是Spring基于ORM框架、JPA规范的基础上封装的一套JPA应用框架，底层使用了Hibernate的JPA技术实现，可使开发者用极简的代码即可实现对数据的访问和操作。它提供了增删改查等在内的常用功能, 且易于扩展。

## 将Spring Data JPA集成到Spring Boot
1. 引入maven依赖包，包括Spring Data JPA和Mysql的驱动
```shell script
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
 <dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>
```
2. 修改application.yml，配置好数据库连接和jpa的相关配置
```shell script
spring:
  datasource:
    url: jdbc:mysql://192.168.1.91:3306/testdb?useUnicode=true&characterEncoding=utf-8&useSSL=false
    username: test
    password: 4rfv$RFV
    driver-class-name: com.mysql.jdbc.Driver
  jpa:
    hibernate:
      ddl-auto: update
    database: mysql
    show-sql: true
```
 `spring.jpa.properties.hibernate.hbm2ddl.auto`是hibernate的配置属性，其主要作用是：自动根据实体类的定义创建、更新、验证数据库表结构。该参数的几种配置如下：
 - `create`：每次加载hibernate时都会删除上一次的生成的表，然后根据你的model类再重新来生成新表，哪怕两次没有任何改变也要这样执行，这就是导致数据库表数据丢失的一个重要原因。
 - `create-drop`：每次加载hibernate时根据model类生成表，但是sessionFactory一关闭,表就自动删除。
 - `update`：最常用的属性，第一次加载hibernate时根据model类会自动建立起表的结构（前提是先建立好数据库），以后加载hibernate时根据model类自动更新表结构，即使表结构改变了但表中的行仍然存在不会删除以前的行。要注意的是当部署到服务器后，表结构是不会被马上建立起来的，是要等应用第一次运行起来后才会。
 - `validate`：每次加载hibernate时，验证创建数据库表结构，只会和数据库中的表进行比较，不会创建新表，但是会插入新值。
