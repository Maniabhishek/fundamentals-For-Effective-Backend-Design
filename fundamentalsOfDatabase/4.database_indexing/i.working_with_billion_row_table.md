> when you are working with billion row table how are we going to improve the performance in this case
> - So if you are trying to find a row inside this table, right, what you can do without the concept of indexing, without acceptance of anything brute force your way, which is do multithreading, do multi processing and chunk the table into multiple segments and search in parallel. Right. That's how basically. Big data essentially and and Hadoop works, right? So it was like map and reduce the subset of the table into smaller concepts. So you can run in parallel and brute force your way and find what you're looking for and try to do the process yourself.
> - another approach add indexing to the table so that we will be able to filter out data with the help of b tree
> - we can also partition table , splitting a whole billion row table into smaller pieces of table , we need to have a logic in place to search from which row to which row , we can do partition based on column like date or region table_europe table_asia
> - similarly we can do sharding (Horizontal Scaling across multiple servers) adding sharding will make query to select the correct shard , then select the correct partition, then do indexing on db and then queried result will be returned


> Splits entire datasets across multiple physical databases or servers.
>- 📌 Each shard contains a portion of the data — typically based on a shard key like user_id % 4.
>- 📌 Often done at the application level or with tools like Citus, MongoDB, CockroachDB, or Vitess.
