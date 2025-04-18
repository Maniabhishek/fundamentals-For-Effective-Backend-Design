### Bitmap Scan vs Index Scan Vs Table Scan

- we have table employees with id and name , executed query ... where id=10000
<img width=800 height=300 src="https://github.com/user-attachments/assets/93ea602a-f4e3-4981-938f-0ed7abcf638e">

  - the moment you do this, Postgres is going to use an index scan using the employees primary key, which is the ID, and then provide the values using the index condition on the index,
  - once we pull that row. Now, the index is responsible to go back to the table to bring the name field. its because the name is part of the heap , part of table (which is part of the heap)

- let's check the query ```select name from employees where id < 100```
  -  I want anything that is less than 100, anything that is lesser than 100, just toss it away. And so it knows that it's going to get values 99 or less because maybe some something was deleted. And as a result, it used an index. And for each value that it finds, it finds the page where that row exists and goes back to the heap to pull that page, which kind of have one or more rows and then pulls that value. And this is called random access.So for 99, it went to the page, it went to the heap, pulled the row. It did that for 98 rows. Okay, So this is called random access.
