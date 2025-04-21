- when you want to create an index in Postgres or in any other database, you specify a field or more than one field to index to create that b-tree on top of it right. And that key will be used for searching purposes. And when you do a search on that index, the database planner, will use that index and search for that. And the entries that found in the index will contain row pointers to point back to the table to fetch the actual rows. where we will have more than one field there.
- Non-key indexes are the abilities, where you can effectively create an index and create Non-key, include some columns inside the index not to search for, but to include. So in this case, if you select like you created an index on the age field, right? And you can optionally include other fields in the index like the ID.
- let's understand it with an example , copied a students.sql filr
```
podman cp ./init.sql pg1:/init.sql
podman exec -it pg1 psql -U postgres
create databsase mydb

podman exec -it pg1 psql -U postgres -d mydb -f /init.sql

```
- to start using students table use below command ```podman exec -it pg1 psql -U postgres -d mydb```
- the above table have millions of rows now we will perform below query
   -  ```explain analyze select id, g from students where g > 8 and g < 90 order by g desc;```
   -  this query will take hell lot of time as g doesn't have any indexing
   -  it took more than 9 seconds , rows removed from by filter , more than 9 millions, since it was seq scan it will be slower
   -  to improve the query we need to do indexing on g

<img width=800 height=300 src="https://github.com/user-attachments/assets/ee76c2fb-ba0e-41c3-a052-ee56d12282e6">

- let's add indexing to g ```create index g_index on students(g);``` and then hit the query ```explain analyze select id, g from students where g> 8 and g<90 order g desc```
  -  will it use the index. We can't guarantee it because the planner has a mind of its own. But let's say they're going to decide to use the index to search for things. But look at what we asked for. We asked for the ID, What is the ID? Well, the ID is actually in two places. The ID is on another index because the primary key and it is also in the heap as another field. So this has to go to the table again to pull the IDs. So you should use the index to pull whatever it needs to pull.
  -  but this still going to take quiet big time even after indexing
  -  let's do indexing ```drop index g_index;``` and add new indexing by including id ```create index g_index on students(g) include (id);```
  -  That's where you as a backend engineer, you really need to think like what columns are you selecting? And based on those columns you create your indexes effectively.
  -  what will happen if i execute my query now ```explain analyze select id, g from students where g> 8 and g<90 order g desc```
  -  it did index only scan after the indexing where we had included id , because of that heap fetches is 0, 
<img width=800 height=300 src="https://github.com/user-attachments/assets/c2e677ca-8ca5-4109-9a49-d93eabe34cdf">
