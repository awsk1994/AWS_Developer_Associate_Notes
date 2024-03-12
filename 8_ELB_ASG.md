# AWS Fundamentals: ELB + ASG

## Scalability

* Scalability means that an application/system can handle greater loads by adapting
* There are 2 kinds of Scalability:
    * vertical scalability
    * horizontal scalability
* Scalability is linked but different to High Availability

### Vertical Scalability
* Increasing the size of the instance
* For example: t2.micro -> t2.large
* is very common for non-distributed systems, such as databases
* RDS, ElastiCache are services that can scale vertically
* There's usually a limit on how much you can vertically scale (hardware limit)

### Horizontal Scalability
* increasing the number of instances/systems for your application
* implies distributed systems
* very common for web application/modern applications
* easy to horizontally scale thanks the cloud offerings, such as Amazon EC2

## High Availability

* High Availability usually goes hand in hand with horizontal sacling
* High availability means running your application/system in at least 2 data centers (== AZs)
* The goal of high availability is to **survive a data center loss**


## ELB (Elastic Load Balancing)
* Load balances are services that forward traffic to multiple servers (eg. EC2 instances) down stream
* Expose a single point of access (DNS) to your application
* Seamlessly handel failures of downstream instances
* Do a regular health checks to your instances
* Provide SLL termination (HTTPS) for your websites
* Enforce stickiness wiht cookies
* Separate public traffic from private traffic
* High availaiblity across zones

### Health Checks
* Health Checks are crucial for load balancers
* They enable the load balancer to know if instances it forwards traffic to are available to reply to requests
* The health check is done on a port and a route (/health is common)

### Types of load balancers on AWS
* Classic Load Balancer
* Application Load Balancer
* Network Load Balancer
* Gateway Load Balancer

## Application Load Balancer (ALB)

* Application Load balancers is Layer 7 (HTTP)
* Load balancing to multiple HTTP applications across machines (target groups)
* Load balancing to mutltiple applications on the same machine (ex: containers)
* Support for HTTP/2 and WebSocket
* Support redirects (from HTTP to HTTPS for example)

* Routing tables to different **target groups**
    * Routing based on path in URL (example.com/users vs example.com/posts)
    * Routing based on hostname in URL 
    * Routing based on Query String, Headers

* ALB are a great fit for microservices & container-based application (eg. Docker & Amazon ECS)
* Has a port mapping feature to redirect to a dynamic port in ECS
* In comparison, we'd need multiple classic load balancer per application

### What are Target Groups?
* EC2 Instances (can be managed by an auto scaling group) - HTTP
* ECS tasks (managed by ECS) - HTTP
* Lambda Functions - HTTP request is translated into a JSON event
* IP Addresses - must be private IPs
* ALB can route to multiple target groups
* Health Checks are at the target group level

### Query String Routing Example
<img src="./img/8_ELB_ASG/1.png"/>

### Good to Know
* You get a Fixed hostname (XXX.region.elb.amazonaws.com)
* The application servers don't see the IP of the client directly
    * the true IP fo the client is inserted in the header **X-Forwarded-for**
    * We can also get Port (X-Forwarded-Port) and proto (X-Forwarded-Proto)

