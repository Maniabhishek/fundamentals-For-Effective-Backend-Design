### lets first discuss about the database schema
- we will be storing id, content, author, metadata
- well we can decouple a few things id, metadata can be stored in one place and id, content can be stored in another place
- id, metadata can be stored in RDBMS , and id , content will preferebly be stored in noSQL db

| id  | author | metadata1 | metadata2 |
|-----|--------|-----------|-----------|

- having all the data seperated will give us querying functionality better

| id  | content |
|-----|---------|

- now tomorrow metadata table will keep on increasing and every time we will have alter table
- to get the last 10 content of a author we need to have sql joins sql joins will also be expensive
- and plus we have id content is noSQL (which dont have sql)
- so we can have metadata dumped inside one json file

| id    | metadata |
|-------|----------|
|       | json     |

- json object with all the metadata
