### HTTP1.1
- this is an application layer protocol
- http1.1 also provides persistent connection, in HTTP1.0 every request required a new connection
```
Request -> TCP Opens
Response -> TCP close
```
- If a webpage had 10 resources, it will require 10 TCP connections
- That was expensive because each connection required **TCP handshake**

### So HTTP/1.1 introduced persistent connections (keep-alive).
```ts
TCP connect
Request 1 → Response 1
Request 2 → Response 2
Request 3 → Response 3
TCP close
```

```
Connection: keep-alive
```
- One connection can handle multiple requests sequentially.
- In HTTP/1.1 this is actually default behavior.

### The Problem with HTTP/1.1
- Even though the connection stays open, there is a limitation.
- Requests must be processed one after another.

#### Example
```ts
Request A
Request B
Request C
```

- Server must respond:
```ts
Response A
Response B
Response C
```

- If Response A is slow, the others must wait.
- This is called: Head of Line Blocking

### HTTP/1.1 Pipelining (Attempted Solution)
- HTTP/1.1 tried to fix this with pipelining.
- Client could send multiple requests without waiting:
```
Request A
Request B
Request C
```
- But responses still had to return in order:
```
Response A
Response B
Response C
```
- If A was slow, B and C still waited.
- Because of this limitation, browsers disabled pipelining.

### What HTTP/2 does differently
- HTTP/2 introduced multiplexing
- instead of sequential requests, HTTP/2 use streams
- Example:
```
Connection
 ├─ Stream 1 → Request A
 ├─ Stream 3 → Request B
 ├─ Stream 5 → Request C
```
- responses can arrive in any order
```
Response B
Response C
Response A
```
- this removes the HTTP-level head of line blocking

- so http1.1 was sequential
```
TCP Connection
  Request A → Response A
  Request B → Response B
  Request C → Response C
```

- HTTP/2 used parallel streams
```
TCP Connection
  Stream 1 → A
  Stream 3 → B
  Stream 5 → C
```

### Why Browsers Open Many Connections in HTTP/1.1
- To work around the limitation, browsers open multiple TCP connections.
- Typical limit, 6 connections per domain
- Example:
```
Connection 1 → HTML
Connection 2 → CSS
Connection 3 → JS
Connection 4 → Image1
Connection 5 → Image2
Connection 6 → Font
```
- HTTP/2 removes this need.

## Key Idea of HTTP/2 
- http/2 solves the problem of head of line blocking by introducing streams
- A single TCP connection can carry multiple can carry multiple independent streams
- think of a streams as a virtual request/response channel inside the same connection
```
TCP Connection
 ├─ Stream 1 → Request /users
 ├─ Stream 3 → Request /orders
 ├─ Stream 5 → Request /products
```
- each request gets a stream ID

### now each streams are split into frames
- HTTP/1.1 operates in a strict "request-response" pair sequence per connection. The server must finish sending the full response for one request before it can send the response for the next request on that same connection.
- HTTP/2 does something very different from HTTP/1.1
- instead of sending entire response at once, it breaks them into frames.
- each frames are tagged with its stream ID
- Example:
- response from /users:
```
Frame 1 (stream 1)
Frame 2 (stream 1)
Frame 3 (stream 1)
```
- response from /orders:
```
Frame 1 (stream 3)
Frame 2 (stream 3)
```
- example transmission
```
Frame(stream 1)
Frame(stream 3)
Frame(stream 1)
Frame(stream 5)
Frame(stream 3)
Frame(stream 1)
```

### Client Reassembles the Responses
- Each frame contains:
    - Stream ID
    - Frame Type
    - Payload
- Example frame:
```
Stream ID: 3
Type: DATA
Payload: "orders..."
```
- Client reads frames and groups them by stream ID.
```
Stream 1 → users response
Stream 3 → orders response
Stream 5 → products response
```
- So responses can complete independently.

### Why One Connection Is Better
- Opening TCP connections is expensive.
- Each connection requires:
- TCP handshake
```
SYN
SYN-ACK
ACK
```
- TLS handshake (for HTTPS)
- Slow start congestion control
- HTTP/2 reduces all this by reusing one connection.

### Flow Control
- HTTP/2 also includes flow control.
- Client can say: Send only 64KB for this stream
- This prevents a single response from blocking the connection.

### Why HTTP/2 Is Much Faster, Benefits:
- Multiplexing
- Single TCP connection
- Header compression (HPACK)
- Binary protocol
- Stream prioritization

### Important Limitation
- Even though HTTP/2 multiplexes streams, it still uses TCP.
- TCP itself has head-of-line blocking at packet level.
- If a packet is lost: TCP must retransmit
- All streams wait
- This is why HTTP/3 was created.
- HTTP/3 uses QUIC over UDP to fix this.

### When Does HTTP/2 Connection Close?
- It can close due to several reasons.
- 1️⃣ Idle timeout
- If no requests happen for some time.
- Typical values:
- System:	Timeout
- Browser:	1–5 minutes
- Load balancer:	30–120 sec
- API gateway:	60 sec
- Example:
- last request → 60 seconds idle → connection closed
- server redeploy or restart
- network interruption





