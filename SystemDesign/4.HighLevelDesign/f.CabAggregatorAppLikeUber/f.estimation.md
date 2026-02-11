### Estimation and Constraints
- Let's start with the estimation and constraints.
- Note: Make sure to check any scale or traffic-related assumptions 

### Traffic
- Let us assume we have 100 million daily active users (DAU) with 1 million drivers and
- on average our platform enables 10 million rides daily.
- If on average each user performs 10 actions (such as request a check available rides,
- fares, book rides, etc.) we will have to handle 1 billion requests daily.
- 100 million × 10 actions = 1 billion/day
- What would be Requests Per Second (RPS) for our system?
- 1 billion requests per day translate into 12K requests per second (1B/24*60*60)= 1B/86400 = 1000000*1000/86400 (and 1M/86400 = 11.57 approx 12) hence 12 k

### Storage
- If we assume each message on average is 400 bytes, we will require about 400 GB of database storage every day.
- 1 billion × 400 bytes = ∼ 400GB /day
- And for 10 years, we will require about 1.4 PB of storage.
- 400 GB × 10 years × 365 days = ∼ 1.4 PB

### Bandwidth
- As our system is handling 400 GB of ingress every day, we will require a minimum bandwidth of around 5 MB per second. 400GB/24*60*60 = 400GB/86400

