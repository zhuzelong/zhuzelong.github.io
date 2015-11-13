---
layout: post
title: CAP on Hbase
categories: [Remarks]
tags: [hadoop]
published: True

---
According to [Wikipedia](https://en.wikipedia.org/wiki/Apache_HBase), Hbase is a "CP" system, which means it has the properties of "Consistency" and "Partition tolerance". It is worth noting that the "consistency" is defined insofar as transactions. Hbase ensures a *BASE* consistency, i.e. **B**asically **A**vailable, **S**oft-state and **E**ventually consistent. The properties make Hbase an elastic database.

I had an impression on "database design specification", i.e. 1NF, 2NF, 3NF and BCNF when I was enrolled in the database course in the university. I found some Hbase instances have a great amount of duplication among tables due to no foreign key or even primary key in the Hadoop world. Therefore, the classical question arises: what will happen when your database violates the normal forms? The first answer is inconsistency. An example of the issue is cascading update and deletion. With foreign keys enabled, you can ensure that the information about an entity is cascading updated or deletion. For example, if a record is removed from the table `Client`, then all tables referencing the table `Client` should remove the corresponding client as well, otherwise something weird would happen. But in the Hadoop world, there is no cascading update and deletion [^1]. As a result, you have to implement them programmatic.

This feature is deemed to be a fundamental in Hadoop but if you forget about it then some issues would probably emerge. So do pay attention to the traditional normal form when you enjoy the "free" NOSQL database.

[^1]: In the Hbase guide, *Cascading* refers to Apache Cascading, an API for manage MapReduce workflow.

