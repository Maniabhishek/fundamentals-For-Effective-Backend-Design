- ICE(interactive connectivity establishment) can manage peer negotiation regarding the most effective way to connect.
- It provides mechanisms for peers to connect directly or, if needed, through a relay using STUN and TURN

### Best Practices for ICE
- Peer Connection: In Peer Connection, it’s easy to connect two applications and use them on two different PCs.
- Make Local Connections a Priority: ICE should prioritize this direct connection for best results if both peers connect to the same local network.
- ICE Timeout Tuning: Finding the right balance between allowing ICE enough time to establish a connection and ensuring users don’t have to wait too long when developing WebRTC solutions. Adapt the timeouts in light of practical testing.
- Concerning Geographical Places: Set up ICE to give preference to servers closer to the user’s location if you’re utilizing several TURN servers. It can cut latency considerably.
