- so to develop the matching users feature we can store this info inside profile service or we can decouple this service and store it inside a new service called matcher service
- this matcher service will store userId to MatchedUserId
- now once we have a match both the users should be able to connect and chat , now when two user matches and tries to establish XMPP over websocket or TCP they see the connection id for give users


![image](https://github.com/user-attachments/assets/86471e91-822e-40a5-8f5e-3be25c9b5d25)


