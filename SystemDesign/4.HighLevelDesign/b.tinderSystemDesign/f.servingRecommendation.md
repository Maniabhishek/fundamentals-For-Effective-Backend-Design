-  all the users data we have it in profile section
-  now we have to recommend the users to client to show them so that they can right swipe of left swipe
-  now we will recommend the users based on age gender and location
-  well we may have millions of user in our db how to choose a perfect db in this case well if we have normal sql db we can still improve and add indexing on these fields to improve the query
-  but still to have these kind of fields we can use cassandra or dynamo db
-  or when we are using any db we can do sharding of db also known as horizontal partitioning, for example user with a to p in one db and q to z in another db this way can reduce the amount of data in one single db which will definetly improve the performance of the query, this is one of the ways
-  what about the single point of failure what if one the db shard fails , are all the data going to be lost , well we can have master slave architecture
-  why are we talking about sharding, well we need to shard the data based on location we are going to be showing the users the relavant data the users in their locations so what our recommendation engine will do get the data based on users gender preference , age preference and location as well create the data table with columns [userid, locations]


<img width=600 height=800 src="https://github.com/user-attachments/assets/01199f29-da3e-4ed2-bc20-d0df0a59da7f">

<img width="1893" height="748" alt="image" src="https://github.com/user-attachments/assets/afbc3f33-bd56-481c-abc2-5a7852103e3a" />
