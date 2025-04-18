- what is indexing
> - An index is is a data structure that you build and you assign on top of an existing table that basically looks through your table and then tries to analyze it and summarize it so that it it can create kind of shortcuts

- simple example like phone book labeled with a, b ,c where all the names starting with a will be stored in that section

## Two type of indexing (these are the data structure which basically help you to search through table effectively)
- b-trees
- LSM trees

-  to understand better we will pull up postgres and create some table

### pull up postgress
```
docker run -e POSTGRES_PASSWORD=postgres --name pg1 postgres
```
 - in another terminal run the below command start postgres in interactive terminal mode
```
docker exec -it pg1 psql -U postgres
```

- create a table employee with id as primary key and name column
``` create table employee(id SERIAL PRIMARY KEY, NAME TEXT NOT NULL);```
``` insert into employees(name) select substr(md5(random()::text), 1, 10) from generate_series(0,1000000);```

- lets try to analyze some query on table
``` explain analyze select name from employees where id=100000 ```
  - now the above query will be faster as id is already indexed as it is a primary key, by indexing it doesn't scan the whole table , wont lookup to the heap but instead goes to binary tree created scans efficiently there

- but what about the below query
``` explain analyze select name from employees where name='abc';```
  - now that name doesn't have indexing it will have scan through the heap or through the table , although postgres will launch multiple workers and can do search in parallel to improve the performance

- with queries like (where name like '%ab%') are the worse query it will look through the table even if there is indexing as like is an expression not a single literal

- let's add indexing to name column
``` create index employees_name on employees(name) ```
  - do the same query again ```explain analyze select name from employees where name='abc'``` this will be faster

<img width=800 hieght=300 src="https://github.com/user-attachments/assets/b85cf352-0288-410d-9b0d-0167112bb5dc">

- let's check the width when we use explain to explain any query
  - this width , The larger this number, the larger the network you're going to take, the higher the TCP packets
  - so if any request has query ```select * from employees``` this will have width higher as we returning the whole table image there are billion table
