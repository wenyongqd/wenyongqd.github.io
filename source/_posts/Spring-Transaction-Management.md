---
title: Spring Transaction Management
date: 2020-08-06 23:32:36
tags:
---

<!-- TOC -->

- [What are Database Transactions ?](#what-are-database-transactions-)
- [What are Application Transactions ?](#what-are-application-transactions-)
- [What is Transaction Management ?](#what-is-transaction-management-)
- [How to implement Transactions Management in Spring Boot ?](#how-to-implement-transactions-management-in-spring-boot-)
- [What are the different types of Transaction Propagations?](#what-are-the-different-types-of-transaction-propagations)
- [What are Transaction Isolation Levels ?](#what-are-transaction-isolation-levels-)

<!-- /TOC -->

## What are Database Transactions ?

A Database transaction is a single logical unit of work which accesses and possibly modifies the contents of a database. It can be considered as a sequence of Queries that should be run in a sequence performing one logical function.
![image](https://www.javainuse.com/trans-min.JPG)

## What are Application Transactions ?

An application transaction is a sequence of application actions that are considered as a single logical unit by the application. For our application the joinOrganization method will be considered as one complete transaction. joinOrganization consists of two actions-

- Persist Employee Information
- Persist HealthInsurance Information
  ![image](https://www.javainuse.com/boot-66-19.JPG)

## What is Transaction Management ?

A transaction manager is a part of an application that controls the coordination of transactions over one or more resources. The transaction manager is responsible for creating transaction objects and managing their durability and atomicity.

## How to implement Transactions Management in Spring Boot ?

In Spring Boot Transaction Management is implemented using Transactional annotation. Transaction is a cross cutting concern and it is implemented using AOP in Spring Boot.
![image](https://www.javainuse.com/boot-66-9-min.JPG)

```java
package com.javainuse.service.impl;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import com.javainuse.model.Employee;
import com.javainuse.model.EmployeeHealthInsurance;
import com.javainuse.service.EmployeeService;
import com.javainuse.service.HealthInsuranceService;
import com.javainuse.service.OrganizationService;

@Service
public class OrganzationServiceImpl implements OrganizationService {

	@Autowired
	EmployeeService employeeService;

	@Autowired
	HealthInsuranceService healthInsuranceService;

	@Override
	@Transactional
	public void joinOrganization(Employee employee, EmployeeHealthInsurance employeeHealthInsurance) {
		employeeService.insertEmployee(employee);
		if (employee.getEmpId().equals("emp1")) {
			throw new RuntimeException("thowing exception to test transaction rollback");
		}
		healthInsuranceService.registerEmployeeHealthInsurance(employeeHealthInsurance);
	}

	@Override
	@Transactional
	public void leaveOrganization(Employee employee, EmployeeHealthInsurance employeeHealthInsurance) {
		employeeService.deleteEmployeeById(employee.getEmpId());
		healthInsuranceService.deleteEmployeeHealthInsuranceById(employeeHealthInsurance.getEmpId());
	}
}
```

Spring Boot implicitly creates a proxy for the transaction annotated methods. So for such methods the proxy acts like a wrapper which takes care of creating a transaction at the beginning of the method call and committing the transaction after the method is executed.
![iamge](https://www.javainuse.com/boot-66-7-min.JPG)

## What are the different types of Transaction Propagations?

The different types of Transaction Propagation for Spring Boot are as follows-

- REQUIRED
- SUPPORTS
- NOT_SUPPORTED
- REQUIRES_NEW
- NEVER
- MANDATORY

## What are Transaction Isolation Levels ?

The Transaction Isolation Levels are as follows-

- READ_UNCOMMITTED
- READ_COMMITTED
- REPEATABLE_READ
- SERIALIZABLE
- DEFAULT
