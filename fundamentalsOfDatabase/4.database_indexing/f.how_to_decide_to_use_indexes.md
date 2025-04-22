### How database optimizers decide to use indexes 
- if there are multiple indexes and you want to know whether your table needs an extra index or not, because if you have multiple indexes, how do you know which index the database is going to use? It's not going to use all of them all the time? It really depends.

> lets say we have a table with two columns with column f1 and f2 , and we have indexing f1_idx and f2_idx on both the columns
>- we want to run a query ``` select * from table where f1="bac" and f2="abc"; ```
>- let's go through some scenarios to see how the database optimizer decides , should it use f1 index or f2 index
>- Let's take case number one, case number one is when the database optimizer decide to use both of them so what it does it queries f1_idx loking for specified value , in this case finding o
>- In this case, finding all the row IDs that matches and tuples in case of Postgres row IDs, in case of Oracle and SQL Server and it collects all these row IDs and then it does the same exact search on the f2 with the specified value "abc" it searches and collects a different set of row IDs and in this case with and it will essentially do an intersection. It essentially merges the results because query has and. You go to the table if necessary, obviously, and you collect the actual values from the table from the heap
>- And if we get too large of a result, if we know that the index is going to turn so many rows, so manyrow IDs, it's just not worth looking through the index In this case, we're going to go through the table index scan.

> let's see another case where database decide to use one index over another. ``` select * from table where f1="bac" and f2="abc"; ```
>- only one index is used
>- eg., f1_idx to search f1="bac" , rowids are collected and the table is accessed and then filtered for f2=4
>- eg., f1 is primary key or stats has low (this condition must be and) database almost always use primary key

> how does database know which one to use when we give query
>- there is something called statistics that is being used by database which kind of help figure out to which case to be used

> Case 3 no index are used (full table scan )
> - database decides the search will yeild so many rows that its going to go to the tabel in the end anyway , so doing table scan will be faster
> - table statistics are critical here
> - these statistics keeps on building as you insert the data lets say we have insrted one row , then 2nd and then third , we also have indexing on one of the columns , and we search for data with where condition in that column , now table is not going to do index scan as db know there are only 3 rows lets get the data by doing table scan
