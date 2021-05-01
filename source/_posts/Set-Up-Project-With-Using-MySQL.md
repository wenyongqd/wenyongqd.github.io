---
title: Set Up Project With Using MySQL
date: 2020-05-23 20:12:38
tags:
---

1. configure `application.properties`
```shell script
spring.jpa.show-sql-true

spring.datasource.url = jdbc:mysql://localhost:3306/ppmtcourse?serverTimezone=UTC
spring.datasource.username = root
spring.datasource.password = 80771696abCD

#Using the right database platform is extremly important on Spring Boot 2.0
spring.jap.database-platform = org.hibernate.dialect.MySQL5Dialect

#CONFLICTS WITH HEROKU from local host
spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.MySQL57Dialect
spring.jpa.hibernate.ddl-auto=update

```
2. 
3. 
4.
5.