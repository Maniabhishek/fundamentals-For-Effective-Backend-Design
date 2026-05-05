- TURN servers are used in instances when STUN fails
- It can occur when both peers are behind firewalls or restrictive NATs.
- Since TURN servers function as a relay between the two peers, any communication will go via them.

- step-by-step procedure of WebRTC with ICE Server Solutions:
  - NAT/firewall constraints prevent Peer A from connecting directly to Peer B.
  - Peer A sends data to the TURN server.
  - After that, Peer B receives this data from the TURN server.
  - Similarly, Peer B sends data to the TURN server, which passes it on to Peer A.
