---
title: Inner Join vs. Outer Join
date: 2020-07-30 22:24:34
tags:
---
<!-- TOC -->

- [Inner Join](#inner-join)
    - [Example of Inner Join](#example-of-inner-join)
- [Outer Join](#outer-join)
    - [Left Outer Join](#left-outer-join)
    - [Left Join Example](#left-join-example)
    - [Right Outer Join](#right-outer-join)
    - [Right Join Example](#right-join-example)
    - [Full Outer Join](#full-outer-join)

<!-- /TOC -->
>In SQL, a join is used to compare and combine — literally join — and return specific rows of data from two or more tables in a database. An inner join finds and returns matching data from tables, while an outer join finds and returns matching data and some dissimilar data from tables.

#### Inner Join
An inner join focuses on the commonality between two tables. When using an inner join, there must be at least some matching data between two (or more) tables that are being compared. An inner join searches tables for matching or overlapping data. Upon finding it, the inner join combines and returns the information into one new table.

##### Example of Inner Join
Let's consider a common scenario of two tables: product prices and quantities. The common information in the two tables is product name, so that is the logical column to join the tables on. There are some products that are common in the two tables; others are unique to one of the tables and don't have a match in the other table.

An inner join on Products returns information about only those products that are common in both tables.
![image](https://static.diffen.com/uploadz/0/00/inner-vs-outer-join_inner.png)

#### Outer Join
An outer join returns a set of records (or rows) that include what an inner join would return but also includes other rows for which no corresponding match is found in the other table.

There are three types of outer joins:

* Left Outer Join (or Left Join)
* Right Outer Join (or Right Join)
* Full Outer Join (or Full Join)

Each of these outer joins refers to the part of the data that is being compared, combined, and returned. Sometimes nulls will be produced in this process as some data is shared while other data is not.

##### Left Outer Join
A left outer join will return all the data in Table 1 and all the shared data (so, the inner part of the Venn diagram example), but only corresponding data from Table 2, which is the right join.

##### Left Join Example
In our example database, there are two products — oranges and tomatoes — on the 'left' (Prices table) that do not have a corresponding entry on the 'right' (Quantities table). In a left join, these rows are included in the result set with a NULL in the Quantity column. The other rows in the result are the same as the inner join.
![image](https://static.diffen.com/uploadz/7/7f/inner-vs-outer-join_outer-left.png)

##### Right Outer Join
A right outer join returns Table 2's data and all the shared data, but only corresponding data from Table 1, which is the left join.

##### Right Join Example
Similar to the left join example, the output of a right outer join includes all rows of the inner join and two rows — broccoli and squash — from the 'right' (Quantities table) that do not have matching entries on the left.
![image](https://static.diffen.com/uploadz/c/c7/inner-vs-outer-join_outer-right.png)

##### Full Outer Join
A full outer join, or full join, which is not supported by the popular MySQL database management system, combines and returns all data from two or more tables, regardless of whether there is shared information. Think of a full join as simply duplicating all the specified information, but in one table, rather than multiple tables. Where matching data is missing, nulls will be produced.
![image](https://static.diffen.com/uploadz/9/9d/inner-vs-outer-join_full-outer.png)