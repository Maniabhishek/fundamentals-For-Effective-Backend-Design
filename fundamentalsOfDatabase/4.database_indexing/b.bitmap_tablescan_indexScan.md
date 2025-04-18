### Bitmap Scan vs Index Scan Vs Table Scan

- we have table employees with id and name , executed query ... where id=10000
<img width=800 height=300 src="https://github.com/user-attachments/assets/93ea602a-f4e3-4981-938f-0ed7abcf638e">

  - the moment you do this, Postgres is going to use an index scan using the employees primary key, which is the ID, and then provide the values using the index condition on the index,
  - once we pull that row. Now, the index is responsible to go back to the table to bring the name field. its because the name is part of the heap , part of table (which is part of the heap)

- let's check the query ```select name from employees where id < 100```
  -  I want anything that is less than 100, anything that is lesser than 100, just toss it away. And so it knows that it's going to get values 99 or less because maybe some something was deleted. And as a result, it used an index. And for each value that it finds, it finds the page where that row exists and goes back to the heap to pull that page, which kind of have one or more rows and then pulls that value. And this is called random access.So for 99, it went to the page, it went to the heap, pulled the row. It did that for 98 rows. Okay, So this is called random access.

- if we do a similar query ```select name from employees where id > 100```
<img width=800 height=300 src="https://github.com/user-attachments/assets/9960ca06-276e-4ea7-8828-e1d40e245335">

  -  as we can see in the image it is doing seq scan but in above query it did index scan as it was faster to scan and look through the heap to find the row but here in this case looking to heap for all the rows which in this case is quiet large in number thus sequential scan is cheaper
 
-  there are two things
  - if we have fewer rows then it does index scan and if we have larger rows then it's way cheaper for me to do a sequential scan on the table because I'm going to go there anyway.
  - In case larger number of rows it dont want to jump read the index and then read the table. Instead just read through the table


#### Bitmap scan 

- In the employee table let's we have another table with age columm
- now we want to run the query ```select name from employees where age > 45```
  - postgres doesn't really know how much but it knows it is quiet large
  - But since there is an index on age. Which is the age. It's worth doing an index scan, but doing an index scan and jumping to the table all the time for every value I find it expensive. So it's going to do instead something called the bitmap index scan.
  - postgres is going to build a bitmap and it's basically an array of bits and the values represent the pagenumber. So bit number zero is page number zero. Bit number one is page number one and so on until the total number of pages.
  - When I find a value that satisfies this condition, I'm going to do an index scan. This is a normal index scan. when I find something, I'm not going to jump directly to the table when I find a page.
  - I'm going to set a bit on that bitmap. So, for example, let's say I found a row, right? And that row belongs to page number nine. So I'm going to go to that bitmap and set bit number nine as one. That means, Hey, by the way, I found a row that in page on page nine and then does goes, goes and through all of the index it scans the whole index. You have a beautiful bitmap that you can use to jump once to the heap table and pull all these pages.
  - Now we're going to do a bitmap scan. So using the number of pages that I know exactly to fetch, I need to jump to the heap once and fetch all those pages. Okay. And when I fetch all those pages, guess what? Every page is going to have one or more row, right? That's how Postgres stores things.
  - Some of those rows will not satisfy the G greater than 995 criteria. So the the Postgres does a recheck on the condition only to filter out the rows that has been filtered and drops the rows that have been filtered. In this case, we were lucky that the exact number of rows actually fit exactly in the in the in the pages.


#### Beauty of bitmap scan 
- So the beauty of the bitmap index scan is you can scan multiple indexes or indices, can scan multiple indexes, build those bitmaps, add them together and then get one beautiful bitmap and then jump to the heap.

- let's take an example ```select name from employees where age > 30 and id < 10000```
  - ID has an index and G has an index.
  - it first did bitmap index scan on age and another bitmap scan on id
  - It will do an index scan, a bitmap index scan on age and calculated that beautiful bitmap that we talked about. And then another bitmap scan on employees_primary key, which is the ID field. Now I have two bitmap what it did. It just anded them.
  - By ending them, any page that exists in one and doesn't exist in the other. don't have to visit it because 100% that row is not going to satisfy my criteria.
