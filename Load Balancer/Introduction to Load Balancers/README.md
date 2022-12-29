# Introduction to Load Balancers
## What is load balancing?
Millions of requests could arrive per second in a typical data center. To serve these requests, thousands (or a hundred thousand) servers work together to share the load of incoming requests.
```
Note: Here, it’s important that we consider how the incoming requests will be divided among all the available servers.
```
A load balancer (LB) is the answer to the question. The job of the load balancer is to fairly divide all clients’ requests among the pool of available servers. Load balancers perform this job to avoid overloading or crashing servers.

The load balancing layer is the first point of contact within a data center after the firewall. A load balancer may not be required if a service entertains a few hundred or even a few thousand requests per second. However, for increasing client requests, load balancers provide the following capabilities:

- Scalability: By adding servers, the capacity of the application/service can be increased seamlessly. Load balancers make such upscaling or downscaling transparent to the end users.
- Availability: Even if some servers go down or suffer a fault, the system still remains available. One of the jobs of the load balancers is to hide faults and failures of servers.
- Performance: Load balancers can forward requests to servers with a lesser load so the user can get a quicker response time. This not only improves performance but also improves resource utilization.

Here’s an abstract depiction of how load balancers work:

[Simplified working of a load balancer](./lbsymplified.jpg)

## Placing load balancers
Generally, LBs sit between clients and servers. Requests go through to servers and back to clients via the load balancing layer. However, that isn’t the only point where load balancers are used.

Let’s consider the three well-known groups of servers. That is the web, the application, and the database servers. To divide the traffic load among the available servers, load balancers can be used between the server instances of these three services in the following way:


```
Place LBs between end users of the application and web servers/application gateway.
Place LBs between the web servers and application servers that run the business/application logic.
Place LBs between the application servers and database servers.
```
[Possible usage of load balancers in a three-tier architecture](./lb_usage.jpg)


In reality, load balancers can be potentially used between any two services with multiple instances within the design of a system.

## Services offered by load balancers
LBs not only enable services to be scalable, available, and highly performant, they offer some key services like the following:

- Health checking: LBs use the heartbeat protocol to monitor the health and, therefore, reliability of end-servers. Another advantage of health checking is the improved user experience.

- TLS termination: LBs reduce the burden on end-servers by handling TLS termination with the client.

- Predictive analytics: LBs can predict traffic patterns through analytics performed over traffic passing through them or using statistics of traffic obtained over time.

- Reduced human intervention: Because of LB automation, reduced system administration efforts are required in handling failures.

- Service discovery: An advantage of LBs is that the clients’ requests are forwarded to appropriate hosting servers by inquiring about the service registry.

- Security: LBs may also improve security by mitigating attacks like denial-of-service (DoS) at different layers of the OSI model (layers 3, 4, and 7).


As a whole, load balancers provide flexibility, reliability, redundancy, and efficiency to the overall design of the system.


```
The heartbeat protocol is a way of identifying failures in distributed systems. Using this protocol, every node in a cluster periodically reports its health to a monitoring service.
```

```
TLS termination, also called TLS/SSL offloading, is the establishment of secure communication channels between clients and servers through encryption/decryption of data.
```

```
Service registry is a repository of the (micro)services and the instances available against each service.
```

```
The DoS is an attack where a client floods the server with traffic to exhaust the server’s resources (processing and/or memory) such that it is unable to process a legitimate user’s request.
```

```
The open systems interconnection (OSI) model is a conceptual framework that divides the problem of connecting any two machines into seven different layers.
```

```
Flexibility: Add or remove machines transparently on the fly.
Reliability: Buggy hosts can be removed through health monitoring which makes the system reliable.
Redundancy: Multiple paths leading to the same destination or failed server’s load is rerouted to the failover machine.
Efficiency: Divide load evenly on all machines to use them effectively from the point of view of the service provider.
```

```
Question
What if load balancers fail? Are they not a single point of failure (SPOF)?

Answer
Load balancers are usually deployed in pairs as a means of disaster recovery. If one load balancer fails, and there’s nothing to failover to, the overall service will go down. Generally, to maintain high availability, enterprises use clusters of load balancers that use heartbeat communication to check the health of load balancers at all times. On failure of primary LB, the backup can take over. But, if the entire cluster fails, manual rerouting can also be performed in case of emergencies.
```

In the coming lessons, we’ll see how load balancers can be used in complex applications and which type of load balancer is appropriate for which use case.
