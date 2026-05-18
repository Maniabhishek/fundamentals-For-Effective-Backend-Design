## token bucket
<img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/9d5e47d0-509f-4155-9a6a-e17fba844fe8" />
### Pros
- Easy to implement
- Memory efficient
### Cons
- Hard to tune the bcuket size and the refill rate properly


## leaky bucket
<img width="300" height="239" alt="image" src="https://github.com/user-attachments/assets/a24e3ff0-2c8f-40e3-9add-d16f45afe273" />
### pros
- Memory effcient.
### Cons
- Recent requests will be blocked and only old requests will be processed when the queue is full.
- Token bucket can send large bursts at a faster rate while leaky bucket always sends requests at constant rate


## fixed window counter

<img width="400" height="249" alt="image" src="https://github.com/user-attachments/assets/aa5195f4-199a-427d-9573-5c5c916731c3" />
### Pros
- Easy to implement
- Memory efficient
### Cons
- A traffic spike at the edges of a window could cause more requests than the allowed quota to go through.


## sliding window log
## sliding window counter
