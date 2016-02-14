# ICCS474
## Internet Programming

### Socket

### The Road to WebSockets

- Polling
    - Ask server in intervals.
    - Pros/Cons?
- Long-polling
    - Ask server once
    - If there is nothing to response, server keep that connection alive until there is something to response.
    - Pros/Cons?
- Server-sent Events (SSEs)
    - One way connection to send data from server to client
    - supported by all major browsers except Internet Explorer (all versions)
    - Serving a client with SSEs requires a persistent connection.
    - Pros/Cons?
- WebSocket
    - More Efficient than SSEs. Metadata are only needed once on the handshake.
    - Full-Duplex
    - http://blog.teamtreehouse.com/an-introduction-to-websockets
    - Still requires a persistent connection.
    - Pros/Cons?

- Keep Alive connection.
- Stream data to client without client triggering the event.
- JS Observer Pattern

- https://github.com/SaKKo/muic-iccs474-2015t2-socket