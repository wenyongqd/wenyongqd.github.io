---
title: Personal Project Management-Backend(1)
subtitle: '"Your problems are tied to wanting to feel good short term. "'

date: 2020-03-21 11:50:32
tags:
  - Spring Boot
  - React
---

<!-- TOC -->

- [Personal Project Management](#personal-project-management)
  - [Project Setup](#project-setup) - [Starting with Spring Initializr](#starting-with-spring-initializr)
  - [Folder Structure](#folder-structure) - [Define a Simple Entity](#define-a-simple-entity) - [Code](#code)
    - [Implementing Validations for RESTful Services](#implementing-validations-for-restful-services)
    - [Refactor Project Controller](#refactor-project-controller)
    - [Custom Exception for Unique Project Identifiers](#custom-exception-for-unique-project-identifiers) - [Additional Knowledge About How to Deal With Exception:](#additional-knowledge-about-how-to-deal-with-exception)
    - [Find Project by Identifier](#find-project-by-identifier)
    - [Find All Projects](#find-all-projects)
    - [Delete an existing project](#delete-an-existing-project)
    - [Update an existing project](#update-an-existing-project)

<!-- /TOC -->

# Personal Project Management

---

## Project Setup

##### Starting with Spring Initializr

**Spring Initializr** -> **Core**(Dev Tools) -> **Web**(Spring Web) -> **SQL**(JPA, MySQL, H2)

## Folder Structure

<img class="shadow" width="280" src="structure.png">

##### Define a Simple Entity

The `Project` class class is annotated with `@Entity`, indicating that it is a JPA entity. (Because no `@Table` annotation exists, it is assumed that this entity is mapped to a table named `Project`.)

The Project object’s `id` property is annotated with `@Id` so that JPA recognizes it as the object’s `ID`. The id property is also annotated with `@GeneratedValue` to indicate that the `ID` should be generated automatically.

#### Code

> **Project**

```java
package io.igileintelliengence.ppmtool.domain;

import javax.persistence.*;
import java.util.Date;

@Entity
public class Project {
    @Id
    @GeneratedValue
    private Long id;
    private String projectName;
    private String projectIdentifier;
    private String description;
    private Date start_date;
    private Date end_date;

    public Project() {
    }

    private Date create_At;
    private Date update_At;

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getProjectName() {
        return projectName;
    }

    public void setProjectName(String projectName) {
        this.projectName = projectName;
    }

    public String getProjectIdentifier() {
        return projectIdentifier;
    }

    public void setProjectIdentifier(String projectIdentifier) {
        this.projectIdentifier = projectIdentifier;
    }

    public String getDescription() {
        return description;
    }

    public void setDescription(String description) {
        this.description = description;
    }

    public Date getStart_date() {
        return start_date;
    }

    public void setStart_date(Date start_date) {
        this.start_date = start_date;
    }

    public Date getEnd_date() {
        return end_date;
    }

    public void setEnd_date(Date end_date) {
        this.end_date = end_date;
    }

    public Date getCreate_At() {
        return create_At;
    }

    public void setCreate_At(Date create_At) {
        this.create_At = create_At;
    }

    public Date getUpdate_At() {
        return update_At;
    }

    public void setUpdate_At(Date update_At) {
        this.update_At = update_At;
    }

    @PrePersist
    protected void conCreate() {
        this.create_At = new  Date();
    }

    @PreUpdate
    protected void onUpdate() {
        this.update_At = new Date();
    }
}
```

Spring `@Repository` annotation is used to indicate that the class provides the mechanism for storage, retrieval, search, update and delete operation on objects.

Spring Repository is very close to `DAO` pattern where DAO classes are responsible for providing CRUD operations on database tables. However, if you are using Spring Data for managing database operations, then you should use Spring Data Repository interface.

> **Repository**

```java
package io.igileintelliengence.ppmtool.repository;

import io.igileintelliengence.ppmtool.domain.Project;
import org.springframework.data.repository.CrudRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface ProjectRepository extends CrudRepository<Project, Long> {
    @Override
    Iterable<Project> findAllById(Iterable<Long> iterable);
}
```

**Here we specify the entity's class and the entity id's class, Project and Long**. When an instance of this repository is instantiated, the underlying logic will automatically be in place for working with our Project class.

> **Service**

```java
package io.igileintelliengence.ppmtool.services;

import io.igileintelliengence.ppmtool.domain.Project;
import io.igileintelliengence.ppmtool.repository.ProjectRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class ProjectService {

    @Autowired
    private ProjectRepository projectRepository;

    public Project saveOrUpdateProject(Project project) {

        return projectRepository.save(project);
    }
}
```

### Implementing Validations for RESTful Services

The validation is a common requirement in all the services. When we get a request to create a user, we should validate its content. If it is invalid, we should return a proper response.

Let's see how to validate a request.
**Step 1**: Open the ProjectController.java file.
**Step 2**: Add **@Valid** annotation in **ProjectController** class. It is a Javax validation API. Its default classpath is spring-boot-starter-web.

- Now we will add validations in **Project** class on **projectName** and **projectIdentifier**. Let suppose that name should have at least five characters and date of birth should be in past not in present.

**Step 3**: Open the Project.java file.
**Step 4**: Add **@NotBlank(message = "Project name is required")** annotation just above the **projectName** variable.
**Step 5**: Add **@NotBlank(message = "Project name is required")
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Size(min=4,max=5,message="Project name is required")
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Column(updatable = false, unique = true)**
annotation just above the **projectIdentifier** variable.
**Step 5**: Open the Rest client Postman and send a `POST` request with new Project. It returns Status: `201 Created`.
![post](post.png)
Now we send another POST request. But the name should have less than five characters. It returns the Status: 400 Bad Request.
![post](post_bad.png)

> **Project**

```java
package io.igileintelliengence.ppmtool.domain;

import com.fasterxml.jackson.annotation.JsonFormat;

import javax.persistence.*;
import javax.validation.constraints.NotBlank;
import javax.validation.constraints.Size;
import java.util.Date;

@Entity
public class Project {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    @NotBlank(message = "Project name is required")
    private String projectName;
    @NotBlank(message = "Project name is required")
    @Size(min=4,max=5,message="Project name is required")
    @Column(updatable = false, unique = true)
    private String projectIdentifier;
    @NotBlank(message = "Project name is required")
    private String description;
    @JsonFormat(pattern = "yyyy-mm-dd")
    private Date start_date;
    @JsonFormat(pattern = "yyyy-mm-dd")
    private Date end_date;
    @JsonFormat(pattern = "yyyy-mm-dd")
    private Date created_At;
    @JsonFormat(pattern = "yyyy-mm-dd")
    private Date updated_At;

    public Project() {
    }

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getProjectName() {
        return projectName;
    }

    public void setProjectName(String projectName) {
        this.projectName = projectName;
    }

    public String getProjectIdentifier() {
        return projectIdentifier;
    }

    public void setProjectIdentifier(String projectIdentifier) {
        this.projectIdentifier = projectIdentifier;
    }

    public String getDescription() {
        return description;
    }

    public void setDescription(String description) {
        this.description = description;
    }

    public Date getStart_date() {
        return start_date;
    }

    public void setStart_date(Date start_date) {
        this.start_date = start_date;
    }

    public Date getEnd_date() {
        return end_date;
    }

    public void setEnd_date(Date end_date) {
        this.end_date = end_date;
    }

    public Date getCreated_At() {
        return created_At;
    }

    public void setCreated_At(Date created_At) {
        this.created_At = created_At;
    }

    public Date getUpdated_At() {
        return updated_At;
    }

    public void setUpdated_At(Date updated_At) {
        this.updated_At = updated_At;
    }

    @PrePersist
    protected void onCreate(){
        this.created_At = new Date();
    }

    @PreUpdate
    protected void onUpdate(){
        this.updated_At = new Date();
    }

}
```

> **Controller**

Then we further customize the exception by following the **BindingResult** interface

The `ResponseEntity` is a class which extends `HttpEntity` and `HttpStatus` class. It is defined in `org.springframework.http.RequestEntity`.

- It is used in `RestTemplate` and `@Controller` methods.
- It is used as parameter in `getForEntity()` and `exchange()` method.

```java
package io.igileintelliengence.ppmtool.web;

import io.igileintelliengence.ppmtool.domain.Project;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.validation.BindingResult;
import org.springframework.validation.FieldError;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import io.igileintelliengence.ppmtool.services.ProjectService;

import javax.validation.Valid;
import javax.validation.constraints.NotNull;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

@RestController
@RequestMapping("/api/project")
public class ProjectController {

    @Autowired
    private ProjectService projectService;

    @PostMapping("/test")
    public ResponseEntity<?> createNewProject(@Valid @RequestBody Project project, BindingResult result){
        Map<String, String> errorMap = new HashMap<>();
        for(FieldError error : result.getFieldErrors()) {
            errorMap.put(error.getField(), error.getDefaultMessage());
        }
        if(result.hasErrors()) {
            return new ResponseEntity<Map<String, String>>(errorMap, HttpStatus.BAD_REQUEST);
        }
        Project project1 = projectService.saveOrUpdateProject(project);
        return new ResponseEntity<Project>(project, HttpStatus.CREATED);
    }
}
```

### Refactor Project Controller

Create a new **MapValidationErrorService** in Service layer.

> **MapValidationErrorService**

```java
package io.igileintelliengence.ppmtool.services;

import io.igileintelliengence.ppmtool.domain.Project;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.stereotype.Service;
import org.springframework.validation.BindingResult;
import org.springframework.validation.FieldError;
import org.springframework.web.bind.annotation.RequestBody;

import javax.validation.Valid;
import java.util.HashMap;
import java.util.Map;
@Service
public class MapValidationErrorService {
    public ResponseEntity<?> MapValidationService(BindingResult result) {

        if (result.hasErrors()) {
            Map<String, String> errorMap = new HashMap<>();
            for (FieldError error : result.getFieldErrors()) {
                errorMap.put(error.getField(), error.getDefaultMessage());
            }
            return new ResponseEntity<Map<String, String>>(errorMap, HttpStatus.BAD_REQUEST);
        }
        return null;
    }
}

```

Inject **MapValidationErrorService** in Controller layer.

```java
package io.igileintelliengence.ppmtool.web;

import io.igileintelliengence.ppmtool.domain.Project;
import io.igileintelliengence.ppmtool.services.MapValidationErrorService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.validation.BindingResult;
import org.springframework.validation.FieldError;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import io.igileintelliengence.ppmtool.services.ProjectService;

import javax.validation.Valid;


@RestController
@RequestMapping("/api/project")
public class ProjectController {

    @Autowired
    private ProjectService projectService;

    @Autowired
    private MapValidationErrorService mapValidationErrorService;

    @PostMapping("/test")
    public ResponseEntity<?> createNewProject(@Valid @RequestBody Project project, BindingResult result){
        ResponseEntity<?> errorMap = mapValidationErrorService.MapValidationService(result);
        if(errorMap != null) return errorMap;

        Project project1 = projectService.saveOrUpdateProject(project);
        return new ResponseEntity<Project>(project1, HttpStatus.CREATED);
    }
}

```

### Custom Exception for Unique Project Identifiers

The **mapValidationErrorService** has no way to check the database that the **Identifier** has already existed. The error may happen when we try to persist to the databae.

```java
Project project1 = projectService.saveOrUpdateProject(project);
```

Create a new package called exceptions, and then we create a **ProjectIdExceptionResponse** and **ProjectIdException** respectively. The **ProjectIdExceptionResponse** is responsible for structuring message.

> **ProjectIdExceptionResponse**

```java
package io.igileintelliengence.ppmtool.exceptions;

public class ProjectIdExceptionResponse {
    private String projectIdentifier;

    public ProjectIdExceptionResponse(String projectIdentifier) {
        this.projectIdentifier = projectIdentifier;
    }

    public String getProjectIdentifier() {
        return projectIdentifier;
    }

    public void setProjectIdentifier(String projectIdentifier) {
        this.projectIdentifier = projectIdentifier;
    }
}

```

> **ProjectIdException**

```java
package io.igileintelliengence.ppmtool.exceptions;

import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.ResponseStatus;

@ResponseStatus(HttpStatus.BAD_REQUEST)
public class ProjectIdException extends RuntimeException {
    public ProjectIdException(String message) {
        super(message);
    }
}

```

When an endpoint returns successfully, Spring provides an `HTTP 200 (OK)` response.

If we want to specify the **response status of a controller method**, we can mark that method with `@ResponseStatus`. It has two interchangeable arguments for the desired response status: code, and value.

```java
@ResponseStatus(HttpStatus.I_AM_A_TEAPOT)
void teaPot() {}
```

> **CustomResponseEntityExceptionHandler**

```java
package io.igileintelliengence.ppmtool.exceptions;

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.context.request.WebRequest;
import org.springframework.web.servlet.mvc.method.annotation.ResponseEntityExceptionHandler;

@ControllerAdvice
@RestController
public class CustomResponseEntityExceptionHandler extends ResponseEntityExceptionHandler {
    @ExceptionHandler
    public final ResponseEntity<Object> handleProjectIdException(ProjectIdException ex, WebRequest request) {
        ProjectIdExceptionResponse exceptionResponse = new ProjectIdExceptionResponse(ex.getMessage());
        return new ResponseEntity(exceptionResponse, HttpStatus.BAD_REQUEST);
    }
}

```

> **ProjectService**

```java
package io.igileintelliengence.ppmtool.services;

import io.igileintelliengence.ppmtool.domain.Project;
import io.igileintelliengence.ppmtool.exceptions.ProjectIdException;
import io.igileintelliengence.ppmtool.repository.ProjectRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class ProjectService {

    @Autowired
    private ProjectRepository projectRepository;

    public Project saveOrUpdateProject(Project project) {

        try {
            project.setProjectIdentifier((project.getProjectIdentifier().toUpperCase()));
            return projectRepository.save(project);
        } catch (Exception e) {
            throw new ProjectIdException("Project ID '"+project.getProjectIdentifier().toUpperCase()+"' already existed");
        }
    }
}

```

The `@ControllerAdvice` annotation was first introduced in Spring 3.2. It allows you to handle exceptions across the whole application, not just to an individual controller. You can think of it as an **interceptor of exceptions thrown by methods annotated with** `@RequestMapping` or one of the shortcuts.
`@ControllerAdvice`注解是一种作用于控制层的切面通知（Advice），能够将通用的`@ExceptionHandler`、`@InitBinder`和`@ModelAttributes`方法收集到一个类型，并应用到所有控制器上。

`@RestControllerAdvice`和`@ExceptionHandler`会捕获所有 Rest 接口的异常并封装成我们定义的 HttpResult 的结果集返回，但是：**处理不了拦截器里的异常**

##### Additional Knowledge About How to Deal With Exception:

1. [Example Link](https://www.kancloud.cn/hanxt/springboot2/1177634).
2. [Exception Handler Demo](https://github.com/zhaojun1998/exception-handler-demo)
3. [Exception Handler Demo2](https://juejin.im/post/5e787ef8f265da571126577c)
4. [Understanding Spring’s @ControllerAdvice](https://medium.com/@jovannypcg/understanding-springs-controlleradvice-cd96a364033f)
5. [Exception Handler Demo3](https://blog.csdn.net/hz_940611/article/details/80737326?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)

> **Result**

![exception](exception.png)

### Find Project by Identifier

> **ProjectRepositor**

Now we create a Find method, JPA will give you a way (**JPQL**) to find by the attributes that are related to the object.

```java
package io.igileintelliengence.ppmtool.repository;

import io.igileintelliengence.ppmtool.domain.Project;
import org.springframework.data.repository.CrudRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface ProjectRepository extends CrudRepository<Project, Long> {

    Project findByProjectIdentifier(String projectId);
}
```

> **ProjectService**

```java
package io.igileintelliengence.ppmtool.services;

import io.igileintelliengence.ppmtool.domain.Project;
import io.igileintelliengence.ppmtool.exceptions.ProjectIdException;
import io.igileintelliengence.ppmtool.repository.ProjectRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class ProjectService {

    @Autowired
    private ProjectRepository projectRepository;

    public Project saveOrUpdateProject(Project project) {

        try {
            project.setProjectIdentifier((project.getProjectIdentifier().toUpperCase()));
            return projectRepository.save(project);
        } catch (Exception e) {
            throw new ProjectIdException("Project ID '"+project.getProjectIdentifier().toUpperCase()+"' already existed");
        }
    }

    public Project findProjectByIndentifer(String projectId) {
        Project project = projectRepository.findByProjectIdentifier(projectId);
        if(project == null) {
            throw new ProjectIdException("Prohect Id does not exist.");
        }
        return project;
    }
}
```

> **ProjectController**

```java
package io.igileintelliengence.ppmtool.web;

import io.igileintelliengence.ppmtool.domain.Project;
import io.igileintelliengence.ppmtool.services.MapValidationErrorService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.validation.BindingResult;
import org.springframework.validation.FieldError;
import org.springframework.web.bind.annotation.*;
import io.igileintelliengence.ppmtool.services.ProjectService;

import javax.validation.Valid;


@RestController
@RequestMapping("/api/project")
public class ProjectController {

    @Autowired
    private ProjectService projectService;

    @Autowired
    private MapValidationErrorService mapValidationErrorService;

    @PostMapping("")
    public ResponseEntity<?> createNewProject(@Valid @RequestBody Project project, BindingResult result){
        ResponseEntity<?> errorMap = mapValidationErrorService.MapValidationService(result);
        if(errorMap != null) return errorMap;

        Project project1 = projectService.saveOrUpdateProject(project);
        return new ResponseEntity<Project>(project1, HttpStatus.CREATED);
    }
    @GetMapping("/{projectId}")
    public ResponseEntity<?> getProjectById(@PathVariable String projectId) {
        Project project = projectService.findProjectByIndentifer(projectId);

        return new ResponseEntity<Project>(project, HttpStatus.OK);
    }

}

```

> **PostMan**

![test2](test2.png)

> **Result**

![test1](test1.png)

### Find All Projects

> **ProjectRepository**

```java
package io.igileintelliengence.ppmtool.repository;

import io.igileintelliengence.ppmtool.domain.Project;
import org.springframework.data.repository.CrudRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface ProjectRepository extends CrudRepository<Project, Long> {

    Project findByProjectIdentifier(String projected);

    @Override
    Iterable<Project> findAll();
}


```

> **ProjectService**

```java
package io.igileintelliengence.ppmtool.services;

import io.igileintelliengence.ppmtool.domain.Project;
import io.igileintelliengence.ppmtool.exceptions.ProjectIdException;
import io.igileintelliengence.ppmtool.repository.ProjectRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class ProjectService {

    @Autowired
    private ProjectRepository projectRepository;

    public Project saveOrUpdateProject(Project project) {

        try {
            project.setProjectIdentifier((project.getProjectIdentifier().toUpperCase()));
            return projectRepository.save(project);
        } catch (Exception e) {
            throw new ProjectIdException("Project ID '"+project.getProjectIdentifier().toUpperCase()+"' already existed");
        }
    }

    public Project findProjectByIndentifer(String projectId) {
        Project project = projectRepository.findByProjectIdentifier(projectId);
        if(project == null) {
            throw new ProjectIdException("Prohect Id does not exist.");
        }
        return project;
    }

    public Iterable<Project> findAllProjects() {
        return projectRepository.findAll();
    }
}
```

> **ProjectController**

```java
package io.igileintelliengence.ppmtool.web;

import io.igileintelliengence.ppmtool.domain.Project;
import io.igileintelliengence.ppmtool.services.MapValidationErrorService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.validation.BindingResult;
import org.springframework.validation.FieldError;
import org.springframework.web.bind.annotation.*;
import io.igileintelliengence.ppmtool.services.ProjectService;

import javax.validation.Valid;


@RestController
@RequestMapping("/api/project")
public class ProjectController {

    @Autowired
    private ProjectService projectService;

    @Autowired
    private MapValidationErrorService mapValidationErrorService;

    @PostMapping("")
    public ResponseEntity<?> createNewProject(@Valid @RequestBody Project project, BindingResult result){
        ResponseEntity<?> errorMap = mapValidationErrorService.MapValidationService(result);
        if(errorMap != null) return errorMap;

        Project project1 = projectService.saveOrUpdateProject(project);
        return new ResponseEntity<Project>(project1, HttpStatus.CREATED);
    }
    @GetMapping("/{projectId}")
    public ResponseEntity<?> getProjectById(@PathVariable String projectId) {
        Project project = projectService.findProjectByIndentifer(projectId);

        return new ResponseEntity<Project>(project, HttpStatus.OK);
    }
    @GetMapping("/all")
    public Iterable<Project> getAllProjects() {return projectService.findAllProjects();}

}
```

> **PostMan**

![postman1](postman1.png)

> **Result**

![Result](result1.png)

### Delete an existing project

> **ProjectService**

```java
package io.igileintelliengence.ppmtool.services;

import io.igileintelliengence.ppmtool.domain.Project;
import io.igileintelliengence.ppmtool.exceptions.ProjectIdException;
import io.igileintelliengence.ppmtool.repository.ProjectRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class ProjectService {

    @Autowired
    private ProjectRepository projectRepository;

    public Project saveOrUpdateProject(Project project) {

        try {
            project.setProjectIdentifier((project.getProjectIdentifier().toUpperCase()));
            return projectRepository.save(project);
        } catch (Exception e) {
            throw new ProjectIdException("Project ID '"+project.getProjectIdentifier().toUpperCase()+"' already existed");
        }
    }

    public Project findProjectByIndentifer(String projectId) {
        Project project = projectRepository.findByProjectIdentifier(projectId);
        if(project == null) {
            throw new ProjectIdException("Project Id '"+projectId+"' does not exist.");
        }
        return project;
    }

    public Iterable<Project> findAllProjects() {
        return projectRepository.findAll();
    }

    public void deleteProjectByIdentifier(String projectid) {
        Project project = projectRepository.findByProjectIdentifier(projectid.toUpperCase());
        if (project == null) {
            throw new ProjectIdException("Cannot Project with ID" +projectid +"'. This Project does not exist.");
        }
        projectRepository.delete(project);
    }
}
```

> **ProjectController**

```java
package io.igileintelliengence.ppmtool.web;

import io.igileintelliengence.ppmtool.domain.Project;
import io.igileintelliengence.ppmtool.services.MapValidationErrorService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.validation.BindingResult;
import org.springframework.validation.FieldError;
import org.springframework.web.bind.annotation.*;
import io.igileintelliengence.ppmtool.services.ProjectService;

import javax.validation.Valid;


@RestController
@RequestMapping("/api/project")
public class ProjectController {

    @Autowired
    private ProjectService projectService;

    @Autowired
    private MapValidationErrorService mapValidationErrorService;

    @PostMapping("")
    public ResponseEntity<?> createNewProject(@Valid @RequestBody Project project, BindingResult result){
        ResponseEntity<?> errorMap = mapValidationErrorService.MapValidationService(result);
        if(errorMap != null) return errorMap;

        Project project1 = projectService.saveOrUpdateProject(project);
        return new ResponseEntity<Project>(project1, HttpStatus.CREATED);
    }
    @GetMapping("/{projectId}")
    public ResponseEntity<?> getProjectById(@PathVariable String projectId) {
        Project project = projectService.findProjectByIndentifer(projectId);

        return new ResponseEntity<Project>(project, HttpStatus.OK);
    }
    @GetMapping("/all")
    public Iterable<Project> getAllProjects() {return projectService.findAllProjects();}

    @DeleteMapping("/{projectId}")
    public ResponseEntity<?> deleteProject(@PathVariable String projectId) {
        projectService.deleteProjectByIdentifier(projectId);
        return new ResponseEntity<String>("Project with ID: '"+projectId+"' was deleted.", HttpStatus.OK);
    }

```

> **Result**

<img class="shadow" width="920" src="ressult3.png" />  
<img class="shadow" width="900" src="result4.png"/>

### Update an existing project

If th id exists, JPA will update the database automatically.
<img class="shadow" width="900" src="result6.png"/>
