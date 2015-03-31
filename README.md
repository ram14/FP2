# Final Project Assignment 2: Explore One More! (FP2) 
DUE March 30, 2015 Monday (2015-03-30)

This is just like FP1, but where you do a different library. (Full description of FP1 is [on Piazza.][piazza])

During this assignment, you should start looking for teammates. See the project schedule [on Piazza.][schedule]

Write your report right in this file. Instructions are below. You can delete them if you like, or just leave them at the bottom.
You are allowed to change/delete anything in this file to make it into your report. It will be public.

This file is formatted with the [**markdown** language][markdown], so take a glance at how that works.

This file IS your report for the assignment, including code and your story.

Code is super easy in markdown, which you can easily do inline `(require net/url)` or do in whole blocks:
```
#lang racket

(require net/url)
```

### My Library: (DB: Database Connectivity)
This library provides database interface for functional programmers.
The Various database it supports are postgreSQL,
MySQL
Oracle
SQL Server,
SQLite Version 3.
This code is important for using database connectivity "(require db)"

To connect to a database of postgresql, the following code is used
(define pgc
    (postgresql-connect #:user user
                        #:database db
                        #:password password))
where user is user name, db is the name of the database to connect to, password is the password. We need these values to connect to a database whether it is postgresql, mysql, oracle, etc.

To execute a query we use query-exec procedure 
In the query-exec we can pass in any database query such as insert, delete, update, etc.
(query-exec pgc
   "create temporary table the_numbers (n integer, d varchar(20))")
   which contains the sql statement in a string.
   
Prepared Statements can be executed multiple times with different parameter values.
   For instance:
   (define get-less-than-pst
    (prepare pgc "select n from the_numbers where n < $1"))
      > (query-list pgc get-less-than-pst 1)
       '(0)
      > (query-list pgc (bind-prepared-statement get-less-than-pst '(2)))
      '(0 1)
      The selected value in here is depended on the argument that is passed to it.

To execute a SQL query, which must produce rows, and returns the list of rows (as vectors) from the query.
 We can use query-rows which takes a connection object like we created pgc in the first point, then takes an sql statement,   it can be any sql query and the third is the argument.
 (query-rows	 	connection	 	 	 	 
 	 	stmt	 	 	 	 
 	 	arg ...	 	 	 	 
 	 [	#:group groupings	 	 	 	 
 	 	#:group-mode group-mode])	
 	 	
To commit a transaction:
 	 	In various web application we need to commit, to finish like online banking.
 	 	In scheme we use:
 	 	(commit-transaction c) → void?
     c : connection?
    If the transaction is valid, it commits otherwise  it raises an exception.

Overall after seeing this library, I came to know how to connect to databases using scheme. It is kind of important because, the whole web development requires. So I learnt a lot out of the research.


1. To start, [**fork** this repository][forking].
1. Modify the README.md file and [**commit**][ref-commit] changes to complete your solution.
  2. (This assignment is just one README.md file, so you can edit it right in github without cloning)
  3. (You may need to clone and push if you want to add extra files)
1. [Create a **pull request**][pull-request] on the original repository to turn in the assignment.

<!-- Links -->
[piazza]: https://piazza.com/class/i55is8xqqwhmr?cid=411
[schedule]: https://piazza.com/class/i55is8xqqwhmr?cid=453
[markdown]: https://help.github.com/articles/markdown-basics/
[forking]: https://guides.github.com/activities/forking/
[ref-clone]: http://gitref.org/creating/#clone
[ref-commit]: http://gitref.org/basic/#commit
[ref-push]: http://gitref.org/remotes/#push
[pull-request]: https://help.github.com/articles/creating-a-pull-request

