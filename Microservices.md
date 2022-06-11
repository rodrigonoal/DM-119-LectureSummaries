# Microservices Architecture - MSA

A way to break the modules of a monolithic application into microservices.

## Monoliths
### Advantages
* Ease of communication between many modules
* More tools - IDEs, for example
* Only one database
* Single deployment

### Problems
* Sometimes alterations in the source code may incur in many side-effects
* A single application that has a lot of responsabilities
* New functionality incurs in more complexity
* Uses more resources to run
* It fails in scallability

## MSA
### What we need
* Separate modules into processes
* Freedom for the developers to choose different programming languages
* Deploy software without stopping the whole application
* How to isolate systems by scope

### Overall characteristics
1. Small
2. Communicate asynchronously (REST, MQTT, AMQP)
3. Dbus or message broker (RabbitMQ, ZeroMQ, Amazon SQS, Kafka)
4. APIs with Swagger or WADL
5. APIs defined by scope
6. Isolate defects
7. Messages must be protected by cryptography
8. Services must be easily swapped
9. Independently installed
10. Autonomous teams

### Load Balancer // API Gateway
* Since microservices act with their own timing, they need orchestration
* The load balancer orchestrates the requisitions for each instance
* Acts as an entry point to your microservices array
* Can be used as an authenticator
* A queue may be used to:
    * organize requests by content
    * buffer requests for a single limited resource
    * switch between differente resources

### Service Discovery
* When you need to start and restart services, the public IPs will change
* Sollution: you will need a service discovery - a service that finds IPs and ports to stablish communication

### Individual Databases
* Each microservice have its own database
* If an information incurs in change to another database, it needs to "ask" another service to do it
* How to deal with inconsistency:
    * Use two-phase commit (2PC) - not ideal
    * Event-based sollution - events are registered on a separate database
    * Log miner - a service that reads the logs and performs updates

### Interpocess Communication IPC
* There may be problems:
    1. Network timeouts
    2. Requisition limitation
* How to deal with them:
    1. Use circuit breaker pattern
    2. Provide fallbacks
    3. Tool: [Hystrix](https://github.com/Netflix/Hystrix)
* Technologies:
    1. Sync or Async calls
        * Async is better for logic decoupling
        * Does not need service discovery
        * Does not need a message buffer (OLT Furukawa)
        * More complex: needs a message broker 
    2. Http based REST / Thrift X AMQP / STOMP
    3. Messages in JSON, XML, binary

### Deployment for MSA
* Single machine:
    * Simple
    * Vulnerable
    * Poor isolation
    * System dependant
* One service per VM or computer:
    * Best isolation
    * Each attends individual necessities
    * Much more expensive
        * Amazon EC2
        * Google Compute Engine
* One service per container:
    * Better isolation
    * Cheaper than many machines
    * Uses Docker, Solaris Zone
    * Can be clustered (Kubernetes)
        * Amazon ECS
        * Google Kubernetes Engine
* Serverless microservices:
    * Much more simple
    * Used on IoT
        * AWS Lambda 
        * Cloud Function

### Migration
1. Stop adding to the monolith
2. Start changing your simplest module into a microservice
    1. Choose the module
    2. Start decoupling - use interfaces
    3. Less detailed interfaces

### Tutorial
[AWS Microservices Tutorial](https://aws.amazon.com/pt/getting-started/hands-on/break-monolith-app-microservices-ecs-docker-ec2/)