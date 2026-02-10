> “This is a real-time collaborative editor where multiple users can edit the same document concurrently. The key challenges are concurrency, conflict resolution, low latency, and consistency.”

- core constraint: Users may:
    - Type at the same position
    - Be offline
    - Receive updates out of order
    - Locks ❌ don’t work (they kill UX).

### High-level collaboration architecture
 Client (Editor) -> ops -> Collaboration Service -> broadcast -> Other Clients

### What flows?
- Not the whole document ❌
- 👉 Operations (insert, delete, replace)
```json
{ "type": "insert", "pos": 5, "char": "A", "user": "u1" }
```

### Concurrency problem
- Scenario, Initial doc:
- - HELLO
- User A inserts X at position 1
- User B deletes E at position 1
- Both happen at the same time.
- ❓ Which one wins?
- ❌ “Last write wins” → data loss
- ❌ Locks → bad UX
- ✅ Use OT or CRDT


### Approach 1: Operational Transformation (OT) (Google Docs uses this)
- Core idea:
- Transform incoming operations based on concurrent operations already applied.
- Example:
    - A: insert X at pos 1
    - B: delete at pos 1
    - If insert arrives first:
    - Delete must shift to pos 2
    - If delete arrives first:
    - Insert shifts to pos 0
- Key concepts to say Each operation has:
    - position
    - version
    - userId
- Server:
    - Maintains operation history
    - Transforms ops before applying
- Pros:
    - Proven (Google Docs)
    - Efficient for text
- Cons:
    - Hard to implement
    - Central server needed
    - Complex edge cases
- “OT preserves user intent instead of blindly applying writes.”

### Approach 2: CRDT (Conflict-free Replicated Data Types) (Used by Figma, Notion, Redis)
- Core idea:
    - Data structures that always converge, no matter operation order.
    - Each character has a unique ID:
    - H(id1) E(id2) L(id3) L(id4) O(id5)
- Insert creates new IDs, ordering is deterministic.
- Properties:
    - No central coordinator needed
    - Works offline
    - Merges automatically
- Pros:
    - Simpler mental model
    - Offline-first
    - Eventual consistency guaranteed
- Cons:
    - Higher memory usage
- Slightly slower for large docs
- “CRDTs guarantee convergence without transformation logic.”

### which one should you use
| Use case                          | Choice   |
| --------------------------------- | -------- |
| Google Docs–scale, central server | **OT**   |
| Offline-first / P2P               | **CRDT** |
| Simpler implementation            | **CRDT** |

### Consistency model
- What consistency?
- ❌ Strong consistency (too slow)
- ✅ Eventual consistency with ordering guarantees
- All users see:
    - Their own edits immediately (local echo)
    - Others’ edits within milliseconds

### How updates flow (step-by-step)
- User types → local edit
- Client:
    - Applies edit immediately
    - Sends operation to server
- Server:
    - Orders operations
    - Transforms / merges
- Broadcasts to other clients
- Clients apply transformed op

### Failure & edge cases (bonus points)
- Network partition → queue ops
- User offline → sync on reconnect
- Cursor position shifts
- Undo/redo across users
- Large documents → chunking / pagination
