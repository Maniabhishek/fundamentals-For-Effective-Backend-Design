<img width=800  height=300 src="https://github.com/user-attachments/assets/e63ed90c-2996-4e39-9d3d-1925aaa5eb79" >

- as in the image we can see it it doing parallel seq scan on students table , which is table scan , where it goes to the table itself and just literally one by one it searches every single row with the given id1
-  we know how to create index on id1 so on creating indexing on id1 it will create b tree on the id1 thus searching will be a bit faster
- lets create the indexing on id1 using command ```create index id1_index on students(id1);```
- and then run ```explain analyze select firstname from students where id1=35446;```
- you may see index scan , and here posgres will use id1_index to search id1 , once it finds that it goes back to the table to actually fetch the value firstname using the reference because that what we are asking for, we are asking for the firstname, and firstname is not in the index and the only value in the index is id1s
- if we change the query to ```explain analyze select id1 from students where id1=35446;``` (although this query doesn't make much sense ) but with this query you will see postgres will do ***index only scan*** which is powerful, it doesn't go back to the table this query is not really useful

<img width=800  height=300 src="https://github.com/user-attachments/assets/789f1fa2-27ae-4151-9f3c-18cbfba40981">

- Index scan are great but index only scans are even better and powerful
- how can we make index only scan more useful
- lets say using this id1 we need to fetch name it is queit more useful then in that case we can drop the id1_index and create another ny including firstname with id1_index command to do so:
   - ```create index id1_index on students(id1) include (firstname)```
- now run ```explain analyze select firstname from students where id1=35446;```
<img width=800  height=300 src="https://github.com/user-attachments/assets/b35c209d-d0ce-43cd-b180-5f35a47c763e">

