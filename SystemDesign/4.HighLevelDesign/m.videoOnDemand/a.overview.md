- Requirements (functional and non functional)
- capacity estimation (traffic, storage, bandwidth)
- Data model (user, video, tags, views)
- type of DB to use
- API design(upload, streaming, listAll, search)
- HLD (User service, Stream service, Search Service, Media Service, Analytics Service)
- inter service communication
- video processing -> file chunker -> content filter -> Transcoder -> quality conversion (360p, 720p, 1080, 1440, 4k)
- why message queue
- video streaming
- searching
- identifying trending content
- sharing
- data partitioning (range based, hash based, list based, composite)
- Geo blocking
- Recommendations
- Metrics
- Analytics
- Caching (eviction policies)


### Identify and resolve bottlenecks

Let us identify and resolve bottlenecks such as single points of failure in our design:
- "What if one of our services crashes?"
    - Running multiple instances of each of our services.
- "How will we distribute our traffic between our components?"
    - Introducing load balancers between clients, servers, databases, and cache servers.
- "How can we reduce the load on our database?"
    - Using multiple read replicas for our databases.
- "How to improve the availability of our cache?"
    - Multiple instances and replicas for our distributed cache.
