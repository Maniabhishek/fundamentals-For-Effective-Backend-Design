### What is a Push Notification?
- A push notification is a message sent from a server → device/app, even when the app is inactive.

### Key property:
- Server initiates communication (not the client polling).

- High-level Architecture (Interview View)
```
[Client App]
     ↓ (register)
[Push Service SDK]
     ↓
[FCM / APNs]
     ↑
[Notification Service]
     ↑
[Business Services / Events]
```

### Core components:
- Client (Mobile / Web)
- Push Provider
- Android / Web → FCM (Firebase Cloud Messaging)
- iOS → APNs
- Notification Service (Backend)

### Event producers (orders, chat, alerts)
- Step-by-step Flow
- Step 1: Device registration
```
App installs

Push SDK generates a device token

App sends token to backend

{
  "userId": "123",
  "deviceToken": "fcm_token_xyz",
  "platform": "android"
}
```
- Step 2: Backend stores token

```
Store in DB:

user_id | device_token | platform | last_seen


One user → multiple devices.
```

- Step 3: Event triggers notification
```
Examples:

New message

Order status update

Payment success
```
- Step 4: Notification service sends push
```
Backend sends request to FCM / APNs with:

Target token(s)

Payload
```
- Step 5: Provider delivers to device
```
Device OS receives message

Shows notification or passes to app

4️⃣ Payload Design (Very Important)
Minimal payload (recommended)
{
  "title": "New Message",
  "body": "You have a new message",
  "data": {
    "chatId": "abc123"
  }
}


Why?

Smaller payload = faster delivery

App fetches full data later
```


### Scaling Considerations (Interview Gold ⭐)
- Fan-out problem
- One event → millions of users
- Solutions:
- Queue (Kafka / SQS / RabbitMQ)
- Worker pool

### Retry & failure handling
- Tokens expire
- Devices offline
- Handle:
- Remove invalid tokens
- Retry with backoff

### Rate limiting
- Push providers enforce limits.Use:
  - Batching
  - Throttling

### Idempotency
- Prevent duplicate notifications:
- (event_id + user_id) unique

### Delivery Guarantees (Important)
- Type	Guarantee
- Push notification	At most once
- Not guaranteed delivery	✔
- Ordering	❌
- Therefore:
- Never rely on push as the only source of truth.

### Security & Privacy
- Tokens are secrets
- Use HTTPS
- Validate ownership
- Allow user opt-out
- Respect quiet hours / DND

### Common Mistakes ❌
- Sending full payload (heavy)
- No retry logic
- Not cleaning dead tokens
- Sending synchronously
- Tying business logic directly to push


