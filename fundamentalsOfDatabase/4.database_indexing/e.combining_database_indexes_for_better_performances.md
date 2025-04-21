- lets hit a query on students table ```explain analyze select lastname from students where g = 70;``` 
- we will see the below analyzation

<img width=800 height=300 src="https://github.com/user-attachments/assets/6b7af5b7-e128-491c-b11c-d798abd4d29e">

- as we can see it has huge number of rows thus postgres to optimize it created bitmap with reference of the table to go back and get the table data
- what will happen if we limit the number of rows,  then in this case it wont create bitmap as it will take some time to do so , hence it will simply do index scan or seq scan directly from the heap as we can see in the image below

> - we create a table called employees with column g_a , g_b , g_c , where we created index on g_a_idx and g_b_idx seperately
<img width=800 height=300 src="https://github.com/user-attachments/assets/16d3ebad-a1b4-479c-9533-1541499e32b4">


> - let's do some query using and
- let's hit query ```explain analyze select lastname from students where g_a=70 and g_b=90;
- it is going to create bitmap on both g_a = 70 and then g_b = 90 , and in the end fetches from bitmap heap
<img width=800 height=300 src="https://github.com/user-attachments/assets/0ce04b9d-f05c-44bd-afd5-92dc7a5d854d">

- as in above queries we had a seperate indexing on g_a and g_b and had condition on both then it was doing bitmap index scan when there are huge number of rows

> - but we can further improve this by combining indexes
- lets first drop g_a_idx and g_b_idx index ```drop index g_a_idx, g_b_idx```;
- let's create composite index using below command
  -  ```create index on employees(g_a, g_b);``` name of index employees_g_a_g_b_idx
  -  So it's going to take longer to create and it's going to be more efficient for queries that have both A and B, especially the ***AND** cases,
  -  let's first query only against g_a ```explain analyze select g_c from employees where g_a=70;```
  -  if you see the below image postgres decided to use employees_g_a_g_b_idx as when we created index g_a was left side
  -  That matters because it's in the left hand side. The values can be easily scanned. That's the Postgres rule. You can scan the values from the left, but you cannot scan them from right. Just the index are built left to right.
  -  when you build that query postgress decided to use the employees_g_a_g_b_idx (composite index) and then jump back to the bitmap heap
  -  when we do a limit it will be even more faster

<img width=800 height=300 src="https://github.com/user-attachments/assets/4151b509-f9de-4b95-ac9d-e4605b9bca48">

-  now lets change the query instead of g_a we will use g_b ```explain analyze select g_c from employees where g_b=70;```

<img width=800 height=300 src="https://github.com/user-attachments/assets/99f05e89-c5bc-4e03-8d01-40ceb41fbbe9">

- look at the change, it is a parallel scan postgres didn't use composite index we created composite index on (g_a, g_b) g_a is left side g_b is not on the left side of tree, this composite index will be used when it's either g_a or (g_a and g_b) when in condition if its only g_b then composite index will not be used
- So if you have a composite index on A and B, querying on B will not use the index. So what the table does, what Postgres does is just jump directly to the table and does a full table scan and using multiple worker threads to do that.

> - how about we use AND in query
- ```explain analyze select g_c from employees where g_a=70 and g_b=90;```
- this query is going to be pretty fast and it will be using composite index as we can see the below image

<img width=800 height=300 src="https://github.com/user-attachments/assets/6f6f28d4-85d0-4ae6-a98c-fc8c3368e28a">


> - how about if we use or query
- ```explain analyze select g_c from employees where g_a=70 or g_b=90;```
- in this situation postgres decided It's useless for to query and try to use that because, you know, it might be faster for me to just to go and jump to the table, do a full table scan instead.

<img width=800 height=300 src="https://github.com/user-attachments/assets/18faf75d-da9c-4e56-9f3f-8989e9016d7e">

> - when we created composite index (g_a , g_b) we saw it was used only when search on g_a or (g_a AND g_b) but it didn't use it when we searched for g_b or (g_a or g_b)
- now let's create index ```create index on employees(g_b)```
- no do the same on g_b this time it will use g_b_idx and also in the case of or case between g_a , g_b

<img width=800 height=300 src="https://github.com/user-attachments/assets/0ee6cd72-f023-4358-b9a9-a10a1308d59a">

<img width=800 height=300 src="https://github.com/user-attachments/assets/7349fa3e-360a-4d19-be48-679f3336fea9">
