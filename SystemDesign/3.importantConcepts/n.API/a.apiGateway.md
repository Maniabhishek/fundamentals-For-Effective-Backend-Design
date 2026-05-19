## API gateway
>- Since we will be using multiple protocols like HTTP, WebSocket, TCP/IP,
deploying multiple L4 (transport layer) or L7 (application layer) type load
balancers separately for each protocol will be expensive. Instead, we can use an
API Gateway that supports multiple protocols without any issues.
>- API Gateway can also offer other features such as authentication, authorization,
rate limiting, throttling, and API versioning which will improve the quality of our
services.
>- We can use services like Amazon API Gateway or Azure API Gateway for this use
case.
