### create index concurrently - avoid blocking production database writes

> Let's say we have a database with huge number of row and we are trying to create index on one of the rows, ```create index ag on employees(ag);```
> - so what happens , here in this postgres will start creating indexing on ag , while it is creating , the writes will be blocked until indexing creation is in progress
> - if you try ```insert into employees values(1);``` you will see this query being blocked when index  creation is in progress

> so in order to avoid that we can create indexing concurrently
> - ```create index concurrently ag on employees(ag)``` creating index concurrently will not block any writes , this is very useful , in case production writes , to avoid blocking it use concurrently creation of index
