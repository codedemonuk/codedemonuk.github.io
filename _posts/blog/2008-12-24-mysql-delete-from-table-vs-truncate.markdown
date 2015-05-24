---
layout: post
title: "MySql Delete From Table vs Truncate"
date: 2008-12-24 18:53:00
author: Pervez Choudhury
categories: 
- Blog
- Development
- MySql
img: php_code.png
thumb: php_code.png
---

Delete from table deletes each row from the one at a time and adds a record into the transaction log so that the operation can be rolled back.  The time taken to delete is also proportional to the number of indexes on the table, and if there are any foreign key constraints (for innodb).

Truncate effectively drops the table and recreates it and can not be performed within a transaction.  It therefore required fewer operations and executes quickly.  Truncate also does not make use of any on delete triggers.

Exact details about why this is quicker in MySql can be found in the [MySql documentation][1]

[1]: http://dev.mysql.com/doc/refman/5.0/en/truncate-table.html