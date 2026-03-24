### since each of the services can have multiple instances , now do we need to load balancer for each of the services
- No, you usually don’t need a separate external load balancer for every service. But yes—load balancing still happens at every layer

### Load Balancing happens in multiple ways , 3 commons patterns:

#### Client side Load balancing
- API Gateway (or service) itself does load balancing
- It talks to a service registry
- No separate LB needed per service
- Logic is inside client (gateway/service)

#### Server side load balancing
- Each service sits behind a load balancer
- you can have LB per service
- But it becomes expensive + operationally heavy

#### Kubernetes / Modern Infra
- you dont explicitly create LB's per service
- Each service gets a ClusterIP / Service abstraction
- Built-in load balancing via:
  - kube-proxy
  - DNS (round-robin)
 
> We don’t necessarily need a dedicated load balancer per service. Instead, we rely on either client-side load balancing using a service registry, or platform-level load balancing (like Kubernetes services). External load balancers are typically only used at the entry point (API Gateway). Internal service-to-service traffic is balanced via service discovery or orchestration layer.”
