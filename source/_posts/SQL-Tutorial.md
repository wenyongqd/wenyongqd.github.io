---
title: SQL Tutorial
date: 2020-07-06 20:19:38
tags:
    - SQL
---

### SQL join
> SQL join 用于根据两个或多个表中的列之间的关系，从这些表中查询数据。

##### Person
| Id_P | LastName | FirstName | Address | City |
| ---- | ---- | ---- | ---- | ---- |
| 1	| Adams	| John | Oxford Street | London |
| 2	| Bush	 | George | Fifth Avenue | New York |
| 3	| Carter | Thomas | Changan Street | Beijing |

##### Order
| Id_O	| OrderNo |	Id_P |
| ---- | ---- | ---- |
| 1	    | 77895	|   3 |
| 2	    | 44678	|   3 |
| 3	    | 22456	|   1 |
| 4	    | 24562	|   1 |
| 5	    | 34764	|   65 |

我们可以通过引用两个表的方式，从两个表中获取数据：
谁订购了产品，并且他们订购了什么产品？

```shell script
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons, Orders
WHERE Persons.Id_P = Orders.Id_P 
```
##### Result
| astName	| FirstName| 	OrderNo |
| ---- | ---- | ---- |
| Adams	| John	 | 22456 |
| Adams	| John	 | 24562 |
| Carter	| Thomas	 | 77895 |
| Carter	| Thomas	 | 44678 |

### 不同的 SQL JOIN
除了我们在上面的例子中使用的 INNER JOIN（内连接），我们还可以使用其他几种连接。
下面列出了您可以使用的 JOIN 类型，以及它们之间的差异。
* JOIN: 如果表中有至少一个匹配，则返回行
* LEFT JOIN: 即使右表中没有匹配，也从左表返回所有的行
* RIGHT JOIN: 即使左表中没有匹配，也从右表返回所有的行
* FULL JOIN: 只要其中一个表中存在匹配，就返回行

##### Reference: [https://www.w3school.com.cn/sql/sql_join_inner.asp]
