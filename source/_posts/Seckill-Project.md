---
title: Seckill Project
date: 2020-07-19 19:18:12
tags:
---

![Image text](seckill.gif)

This project simulate the hign concurrency scenario, it includes the following technologies:

- Build a full stack project using **Spring Boot** in backend, **Vue.js** and Redux on the front end
- Implement rack-attack (based on **Redis**) to limit robots-access and different API requests
- Use two times **MD5** (password encryption) and distributed session to implement register and login function
- Use Redis and **Kafka** for asynchronous communication to optimize seckill system

## Dependent frameworks and packages

1. [Spring Boot](https://spring.io/projects/spring-boot) Web framework and server
1. [Spring Data JPA](https://spring.io/projects/spring-data-jpa) Access database
1. [Spring Data Redis](https://spring.io/projects/spring-data-redis) Cache data
1. [Spring Security](https://spring.io/projects/spring-security) Authenticate and authrorize
1. [Spring Session](https://spring.io/projects/spring-session) Manage session
1. [GraphQL Java](https://github.com/graphql-java/graphql-java) Graphql for java
1. [Extended Scalars](https://github.com/graphql-java/graphql-java-extended-scalars) Extended scalars for graphql java
1. [Flyway](https://flywaydb.org/) Database migration
1. [Swagger](https://swagger.io/) Api documentation

## APIs

### Rest

| Path  | Method | Description |
| ------------- | ------------- | ------------- |
| /auth/login | POST | Login |
| /auth/logout | GET | Logout |
| /auth/logged | GET | Get logged user |
| /user/register | POST | Register |
| /user/modify | POST | Modify logged user |
| /user/info | GET | Get user info |
| /user/follow | POST | Follow user |
| /user/unfollow | POST | Unfollow user |
| /user/following | GET | Following users of someone |
| /user/follower | GET | Fans of some user |
| /user/sendMobileVerifyCode | POST | Send mobile verify code |
| /post/publish | POST | Publish post |
| /post/delete | POST | Delete post |
| /post/info | GET | Get post info |
| /post/published | GET | Get published posts of some user |
| /post/like | POST | Like post |
| /post/unlike | POST | Unlike post |
| /post/liked | GET | Liked posts of some user |
| /post/following | GET | Posts of following users of someone |
| /file/upload | POST | Upload file |
| /file/info | GET | Get file meta info |

## How to run

This project need java v11+.

### By local environment

#### Clone repository

```bash
https://github.com/wenyongqd/seckil_backend.git
```

#### Prepare mysql, kafka, redis and zookeeper service
