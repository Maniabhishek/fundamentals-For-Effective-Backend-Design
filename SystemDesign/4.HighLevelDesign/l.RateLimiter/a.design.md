# token bucket
<img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/9d5e47d0-509f-4155-9a6a-e17fba844fe8" />
### Pros
- Easy to implement
- Memory efficient
### Cons
- Hard to tune the bcuket size and the refill rate properly


# leaky bucket
<img width="300" height="239" alt="image" src="https://github.com/user-attachments/assets/a24e3ff0-2c8f-40e3-9add-d16f45afe273" />
### pros
- Memory effcient.
### Cons
- Recent requests will be blocked and only old requests will be processed when the queue is full.
- Token bucket can send large bursts at a faster rate while leaky bucket always sends requests at constant rate


# fixed window counter

<img width="400" height="249" alt="image" src="https://github.com/user-attachments/assets/aa5195f4-199a-427d-9573-5c5c916731c3" />
### Pros
- Easy to implement
- Memory efficient
### Cons
- A traffic spike at the edges of a window could cause more requests than the allowed quota to go through.


# sliding window log
- lets understand:
- 5 requests per 60 seconds
- [10, 20, 30, 40, 50]
- Now request comes at: time = 65
- Step 1: Remove old entries, Window is: 65 - 60 = 5
- Remove timestamps older than 5.
- Remaining: [10, 20, 30, 40, 50]
- (all still valid)
-Step 2: Count requests Count: 5 , Limit reached.
- 👉 Reject request ❌
-Now request at: time = 71 window: 71 - 60 = 11
- Remove: 10 , Remaining: [20, 30, 40, 50]
- Count: 4, 👉 Allow request ✅
- Add: 71
- New log: [20, 30, 40, 50, 71]

### Data Structure Used , Usually:
- Queue
- Deque
- Redis sorted set

### Pros
- Very accurate
- Smooth rate limiting
- No burst issue like fixed window

### cons
- memory Heavy
- Stores every request timestamp
- expensive for huge scale

# sliding window counter
