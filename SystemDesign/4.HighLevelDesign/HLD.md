- You should start with the functional requirements first—that is, the core product features and use cases that the system needs to support.
- Want speed, use a cache. Want availability, put in some redundancy. Want fast reads to db, use a read replica. Want fast writes to db, use sharding.

- How to Get Yourself Unstuck Tip #1 - To simplify the problem, think about the data in the problem as immutable. You can choose to add mutability back in later after you have an initial working design.
- How to Get Yourself Unstuck Tip #2 - Ask your interviewer: “Are there any important requirements you have in mind that I’ve overlooked?”

- How to Get Yourself Unstuck Tip #3 - Ask your interviewer if they’d like to see some calculations before jumping in and starting them—you might be able to skip these entirely if the interviewer doesn’t care about it!

- How to Get Yourself Unstuck Tip #4 - Follow these rough guides to get the basic estimates for any system
  - Storage Estimation
  - Traffic
  - Bandwidth Estimation (Bandwidth = Requests per second × Data per request)
  - calculate processing power of any of the services (amount_of_data_ingested_in_that_service * read_per_mb * ) = total_reads per mb <=> now to calculate time it will take to process , assume each reads will few millisecs lets say 20ms then => total_reads_per_mb * time_to_process_1_mb
- How to Get Yourself Unstuck Tip #5 “Would it be fine if the data in my system was occasionally wrong for a split second or so?”
  -  If the answer is yes, then you probably want eventual consistency.
  -  If the answer is no, then you’re looking for a strong consistency called linearizability.


### Functional
- Start with the customer and work backwards
- Who will use the system
- How the system will be used
- Choosing just the top 3 features
- Adding features that are out of scope is a nice to have, it shows product thinking
- Ask your interviewer: “Are there any important requirements you have in mind that I've overlooked?”

### Non functional
- High availability
- Scalability
- Performance ( in terms of latency and throughput)
- Rezilience (is how quickly the system can recover from failures)
- Durability (backups, replication)
- Consistency
- Maintainability (monitoring , testing , deployment, Failure modes and mitigations)
- Security (CostEngineering cost Maintenance cost Resource cost)

### API design (5-7mins)
High level design (10-15mins)

### Deep dives (15-20 min)
- Scaling the high level design
- Scaling individual components:
- Availability, Consistency and Scale story for each component
- Consistency and availability patterns
- Think about the following components, how they would fit in and how it would help:
    - Client (Mobile, Browser)
    - DNS

    - CDN (Push vs Pull)
    - Load Balancers (Active-Passive, Active-Active, Layer 4, Layer 7)
    - Reverse Proxy
    - Blob Storage
    - Application layer scaling (Microservices, Service Discovery, N
tier)
    - Database:
        -  SQL
            -  Replication, Sharding, Indexing, Denormalization, SQL Tuning
        - NoSQL
            - Types: Key-Value, Wide-Column, Graph, Document,
Geospatial, Vector, Full-Text scanning
        - Read heavy: MongoDB, Couchbase
        - Write heavy: Cassandra, ScyllaDB
    - Cold/Hot storage
    - Cache:
        - Client caching, CDN caching, Webserver caching, Database caching, Application caching
        - Eviction policies: LRU, LFU
        - Types: Cache aside, Write through, Write behind
    - Queue:
        - Message queues
        - Task queues
        - Back pressure
- Logging, Metrics and Automation

- Communication:
    - HTTP/S, TCP, UDP, RPC, Web Sockets
- Logging, Metrics and Automation

### Estimations (3–5 min) (ask interviewer if needed)
- Latency/Throughput expectations
- QPS (Queries Per Second) Read/Write ratio
- Total/Daily active users
- Traffic estimates
    - Write (QPS, Volume of data)
    - Read (QPS, Volume of data)
- Storage estimates
- Memory estimates
    - If we are using a cache, what is the kind of data we want to store in cache
    - How much RAM and how many machines do we need for us to achieve this?
    - Amount of data you want to store in disk/ssd
 
### Follow-up (2–3 min)
- Bottlenecks
- SPOF
- Latency (use other protocols, cache, multi-threading, faster algorithms, compression, cdn)
- Security
- Cost
- Error cases (server failure, network loss, etc.) and how to handle them
- Monitoring
- How to scale the system to the next level
