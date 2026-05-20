-  think about functional and non-functional requirements
-  is it a distributed system (high level user-> global LB -> Regional LB -> services -> DB)
-  api gateways, auth service, profile service, service mapper, 


Client
   ↓
Load Balancer
   ↓
WebSocket Gateway / Chat Gateway
   ↓
Authentication validation
   ↓
Persistent WebSocket connection established
   ↓
Connection stored
   ↓
Messages routed through messaging infrastructure
