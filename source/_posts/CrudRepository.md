---
title: CrudRepository
subtitle: "\"Focus on Learning and Creating, Not Entertainment and Distraction.\""
date: 2020-03-22 12:45:50
tags:
---
> Discomfort is how we grow.

<img class="shadow" width="1000" src="https://miro.medium.com/max/2410/1*Q7FUXblFAgfYM6nnxqdY5g.jpeg">

### Core Concepts
The central interface in Spring Data repository abstraction is Repository (probably not that much of a surprise). It takes the the domain class to manage as well as the id type of the domain class as type arguments. This interface acts primarily as a marker interface to capture the types to work with and to help you to discover interfaces that extend this one. The CrudRepository provides sophisticated CRUD functionality for the entity class that is being managed.
**Example 1.1. CrudRepository interface**
```java
public interface CrudRepository<T, ID extends Serializable>
    extends Repository<T, ID> {
                                                                                                                       (1)
    <S extends T> S save(S entity);                             ❶
                                                                                                                       (2)
    T findOne(ID primaryKey);                                   ❷
                                                                                                                       (3)
    Iterable<T> findAll();                                      ❸

    Long count();                                               ❹
                                                                                                                       (4)
    void delete(T entity);                                      ❺
                                                                                                                       (5)
    boolean exists(ID primaryKey);                              ❻
                                                                                                                       (6)
    // … more functionality omitted.
}
```
❶	Saves the given entity.
❷   Returns the entity identified by the given id.
❸   Returns all entities.
❹   Returns the number of entities.
❺   Deletes the given entity.
❻   Indicates whether an entity with the given id exists.



#### Folder Structure
<img class="shadow" width="280" src="structure.png">

#### Configure the Deployment Descriptor - “application.properties”
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/spring_boot
spring.datasource.username=root
spring.datasource.password=80771696abCD
spring.datasource.driverClassName=com.mysql.jdbc.Driver
spring.jpa.database=MySQL
spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=update
spring.jpa.hibernate.naming-strategy=org.hibernate.cfg.ImprovedNamingStrategy
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
```
- Automatic schema generation
    - `create-only`: Database creation will be generated.
    - `drop`: Database dropping will be generated.
    - `create`: Database dropping will be generated followed by database creation.
    - `create-drop`: Drop the schema and recreate it on SessionFactory startup. Additionally, drop the schema on SessionFactory shutdown.
    - `validate`: Validate the database schema.
    - `update`: Update the database schema

#### Code

> **User**

```java
package com.example.jpa.domain;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;
@Entity
@Table(name = "t_user")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Integer userId;
    private String userName;
    private String sex;
    private Integer age;
    public Integer getUserId() {
        return userId;
    }
    public void setUserId(Integer userId) {
        this.userId = userId;
    }
    public String getUserName() {
        return userName;
    }
    public void setUserName(String userName) {
        this.userName = userName;
    }
    public String getSex() {
        return sex;
    }
    public void setSex(String sex) {
        this.sex = sex;
    }
    public Integer getAge() {
        return age;
    }
    public void setAge(Integer age) {
        this.age = age;
    }
}

```
> **UserRepository**

```java
package com.example.jpa.repository;

import com.example.jpa.domain.User;
import org.springframework.data.repository.CrudRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface UserRepository extends CrudRepository<User, Integer> {

}
```
> **UserController**

```java
package com.example.jpa.controller;

import javax.annotation.Resource;

import com.example.jpa.domain.User;
import com.example.jpa.service.UserService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;


@RestController
@RequestMapping("/user")
public class UserController {
    @Autowired
    private UserService userService;
    @RequestMapping("/save")
    public String save() {
        User user=new User();
        user.setUserName("jack");
        user.setSex("男");
        user.setAge(22);
        userService.save(user);
        return "数据添加成功!";
    }

    @RequestMapping("/delete")
    public String delete() {
        userService.delete(2);
        return "删除成功!";
    }

    @RequestMapping("/update")
    public String update() {
        User user=userService.getById(3);
        userService.update(user);
        return "更新成功!";
    }

    @RequestMapping("/getAll")
    public Iterable<User> getAll(){
        return userService.getAll();
    }
}

```

> **UserService**

```java
package com.example.jpa.service;

import java.util.Optional;
import javax.transaction.Transactional;
import com.example.jpa.domain.User;
import com.example.jpa.repository.UserRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;
    @Transactional
    public User save(User user) {
        return userRepository.save(user);
    }

    @Transactional
    public void delete(Integer id) {
        userRepository.deleteById(id);
    }

    @Transactional
    public void update(User user) {
        user.setUserName("露丝");
        user.setAge(23);
    }

    public User getById(Integer id) {
        Optional<User> op=userRepository.findById(id);
        return op.get();
    }

    public Iterable<User> getAll(){
        return userRepository.findAll();
    }
}

```
[Reference](https://blog.csdn.net/dwenxue/article/details/82855550)