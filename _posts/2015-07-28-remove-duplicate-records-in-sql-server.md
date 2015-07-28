---
layout: post 
title: Remove duplicate records in SQL Server
categories: [Record]
tags: [SQL]
published: True

---
## Question

As my last post stated, there are duplicate records in my database so I tried to remove these duplications. Note that the `ID` of duplicate rows are unique since the column `ID` is defined as `uniqueidentifier`.


## Solution

I tried to remove duplication by comparing datetime using window function. As a result, my queries were almost overflow in lock or memory. I then looked for solutions on StackOverflow and posted my own question. The following posts would probaby help.

- [How can I remove duplicate rows?](http://stackoverflow.com/questions/18932/how-can-i-remove-duplicate-rows)
- [My question](http://stackoverflow.com/questions/31658294/how-to-remove-duplicate-rows-in-sql-server?noredirect=1#comment51264627_31658294)

It is necessary to clarify *remove duplication*. One can either delete rows from the original table or select unique rows into a new table. As a rule of thumb, avoid **deleting** data from database. Therefore, I selected unique rows into another table.


## Summary

1. Be cautious about `ROW_NUMBER()` function for big data. I used `ROW_NUMBER()` and the query took over 14 hours without results (I stopped the query).
2. Never forget the objective. My initial objective is to remove duplicate rows then I spent a few days struggling with `DATEDIFF` function and controlling memory usage while the solution is simple and fast (an aggregation function `MIN` with `GROUP BY`).