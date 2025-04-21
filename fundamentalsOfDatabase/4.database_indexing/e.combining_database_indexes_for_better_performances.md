- lets hit a query on students table ```explain analyze select lastname from students where g = 70;``` 
- we will see the below analyzation

<img width=800 height=300 src="https://github.com/user-attachments/assets/6b7af5b7-e128-491c-b11c-d798abd4d29e">

- as we can see it has huge number of rows thus postgres to optimize it created bitmap with reference of the table to go back and get the table data
- what will happen if we limit the number of rows,  then in this case it wont create bitmap as it will take some time to do so , hence it will simply do index scan or seq scan directly from the heap as we can see in the image below

<img width=800 height=300 src="https://github.com/user-attachments/assets/16d3ebad-a1b4-479c-9533-1541499e32b4">


> - let's do some query using and
- let's hit query ```explain analyze select lastname from students where g_a=70 and g_b=90;
- it is going to create bitmap on both g_a = 70 and then g_b = 90 , and in the end fetches from bitmap heap 
