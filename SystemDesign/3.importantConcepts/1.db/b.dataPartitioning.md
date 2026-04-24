### Data Partitioning
> To scale out our databases we will need to partition our data. Horizontal partitioning
(aka Sharding) can be a good first step. We can use partitions schemes such as:
10
- Hash-Based Partitioning
- List-Based Partitioning
- Range Based Partitioning
- Composite Partitioning

- The above approaches can still cause uneven data and load distribution, we can solve this using Consistent hashing.
