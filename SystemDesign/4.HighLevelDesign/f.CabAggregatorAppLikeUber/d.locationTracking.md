### Location Tracking
> How do we efficiently send and receive live location data from the client (customers
> and drivers) to our backend? We have two different options:
### Pull model
> The client can periodically send an HTTP request to servers to report its current
> location and receive ETA and pricing information. This can be achieved via something
> like Long polling.
### Push model
> The client opens a long-lived connection with the server and once new data is
> available it will be pushed to the client. We can use WebSockets or Server-Sent
> Events (SSE) for this.
> The pull model approach is not scalable as it will create unnecessary request
> overhead on our servers and most of the time the response will be empty, thus
> wasting our resources. To minimize latency, using the push model with WebSockets
> is a better choice because then we can push data to the client once it's available
> without any delay, given that the connection is open with the client. Also,
> WebSockets provide full-duplex communication, unlike Server-Sent Events (SSE)
> which are only unidirectional.
> Additionally, the client application should have some sort of background job
> mechanism to ping GPS location while the application is in the background.
> Note: Learn more about Long polling, WebSockets, Server-Sent Events (SSE).
