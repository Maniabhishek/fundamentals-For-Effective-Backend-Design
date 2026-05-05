### what exactly happens when you are using http2.0, how does it multiplexes , how requests are ordered
> lets understand step by step from connection -> frames -> streams -> bytes -> reconstruction

### First Layer: TCP connection
- HTTP/2 runs on top of TCP.
- connection stack:
```ts
HTTP/2
TLS
TCP Handshake
IP
```
- when a client connects: Client → TCP handshake → Server
- TCP guarantees:
```
ordered byte delivery
reliable delivery
```
- So the server receives exactly the same byte sequence the client sent.
- ### HTTP/2 Replaces Text With Binary Frames
- In HTTP/1.1 the request looks like this:
- GET /users HTTP/1.1 (it is a plain text based protocol)
- Host: api.example.com
- This is text based.
- HTTP/2 converts everything into binary frames.
- Every message is split into frames like:
- +-----------------------------------------------+
- | Length | Type | Flags | Stream ID | Payload   |
- +-----------------------------------------------+
- Frame header size:
- 9 bytes

| Field             | Size     |
| ----------------- | -------- |
| Length            | 3 bytes  |
| Type              | 1 byte   |
| Flags             | 1 byte   |
| Stream Identifier | 4 bytes  |
| Payload           | variable |

### What is stream 
- A stream represents one request-response pair.
```
Stream 1 → GET /users
Stream 3 → GET /orders
Stream 5 → GET /products
```
- Each stream has a unique stream ID.
```
client uses odd numbers
server uses even numbers
```
```
Stream 1
Stream 3
Stream 5
```

### Frames Belong to Streams
- A request or response is broken into multiple frames.
- Example request:
- GET /users
- Becomes:
```
Frame 1 → HEADERS (stream 1)
Frame 2 → DATA (stream 1)
Frame 3 → DATA (stream 1)
```
- Another request:
- GET /orders
- Becomes:
```
Frame 4 → HEADERS (stream 3)
Frame 5 → DATA (stream 3)
```

### Multiplexing Happens at Frame Level
- Instead of sending complete messages sequentially, HTTP/2 interleaves frames.
- Example transmission over TCP:

```
Frame(stream1)
Frame(stream3)
Frame(stream1)
Frame(stream5)
Frame(stream3)
Frame(stream1)
```
- So frames from multiple streams share the same connection. This is multiplexing.

### Byte-Level Transmission
- Suppose we send these frames:
```
Frame A → stream 1 → 1000 bytes
Frame B → stream 3 → 500 bytes
Frame C → stream 5 → 700 bytes
```
- Actual TCP byte stream might look like:
```
[A header][A payload]
[B header][B payload]
[C header][C payload]
[A header][A payload]
[B header][B payload]
```
- To TCP, it is just a continuous byte stream.

- Example raw bytes:
```
0003E8 01 04 00000001 <payload>
0001F4 01 04 00000003 <payload>
0002BC 01 04 00000005 <payload>
```
- The server reads these bytes sequentially.

### Server Frame Parser
- Server reads bytes from TCP socket:
- read 9 bytes → frame header
- From header it learns:
```
frame length
frame type
stream ID
```
- Example:
```
length: 1000
type: DATA
stream: 3
```
- Server then reads:
- next 1000 bytes → payload
- Now it knows:
- this payload belongs to stream 3

### Stream Reassembly
- Server maintains a stream table.
- Example:
```
streams = {
 1: requestA,
 3: requestB,
 5: requestC
}
```
- When frames arrive:
```
Frame(stream1) → append to stream1 buffer
Frame(stream3) → append to stream3 buffer
Frame(stream1) → append to stream1 buffer
```
- Eventually the request becomes complete.

### Flow Control
- HTTP/2 adds flow control windows.
- Example:
- client window = 64KB
- Server cannot send more data until client allows.
- Frame used:
- WINDOW_UPDATE
- This prevents one stream from starving others.

### Why This Improves Performance
- Multiplexing removes:
- connection overhead
- TCP slow start per connection
- head-of-line blocking at HTTP layer
- One connection efficiently carries all data.


























