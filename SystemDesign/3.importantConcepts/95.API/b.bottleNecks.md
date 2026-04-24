## Identify and resolve bottlenecks
- Let us identify and resolve bottlenecks such as single points of failure in our design:
  1. "What if one of our services crashes?"
  2. "How will we distribute our traffic between our components?"
  3. "How can we reduce the load on our database?"
  4. "How to improve the availability of our cache?"
  5. "Wouldn't API Gateway be a single point of failure?"
  6. "How can we make our notification system more robust?"
  7. "How can we reduce media storage costs"?
  8. "Does chat service has too much responsibility?"
- To make our system more resilient we can do the following:
  1. Running multiple instances of each of our services.
  2. Introducing load balancers between clients, servers, databases, and cache servers.
  3. Using multiple read replicas for our databases.
  4. Multiple instances and replicas for our distributed cache.
  5. We can have a standby replica of our API Gateway.
  6. Exactly once delivery and message ordering is challenging in a distributed system,
  we can use a dedicated message broker such as Apache Kafka or NATS to make
  our notification system more robust.
  7. We can add media processing and compression capabilities to the media service to compress large files similar to WhatsApp which will save a lot of storage space
  and reduce cost.
  8 We can create a group service separate from the chat service to further decouple our services.
