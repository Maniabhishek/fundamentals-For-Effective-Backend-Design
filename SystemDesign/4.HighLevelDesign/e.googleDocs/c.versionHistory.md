### how are we going to deal with version history 
- let say a user types something and this latest changes need to be sent to server in order to be stored to db
- now for example we have documents below

| id | content |
|----|---------|
| 1  | ABC     |

- now this content is being changed to ABCD

| id | content |
|----|---------|
| 1  | ABCD    |

- again this document gets changed ABCDE and db becomes

| id | content |
|----|---------|
| 1  | ABCDE   |

-  what we need to do here is we need to develop a feature where we can server user all the history of changes
-  so we will also store the version history

| id | version | content |
|----|---------|---------|
| 1  | 1       | ABC     |

- then changes to ABCD

| id | version | content |
|----|---------|---------|
| 1  | 2       | ABCD    |

- then ABCDE

| id | version | content |
|----|---------|---------|
| 1  | 3       | ABCDE   |

- what we can also do is can merge the id with version create a unique key of versions 1_1, 1_2, 1_3
- so now what we will do everytime user lets say save the file we will directly save this document to content table
- now we will have cron job which may run every 30 mins create a new version history of the current file with given data in table
- now running cron job in every 30 mins can cause thundering herd in db
- instead we will maintain the timestamp , and will only update the documents version history which were updated in last 30 minutes
