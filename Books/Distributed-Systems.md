## Designing Distributed Systems
---
### Chapter 1.: Side Car Pattern
Definition - A container that augments a pre-existing container to add functionality
* Examples:
    - nginx container used to provide https services to legacy application running on http
    - container that synchronizes a git repo and local file system on a server with most up to date files
* Notes:
    - container modularity extremely important
    - container should be reusable across most applications
    - container should have a consisten API not susceptible to breaking changes
    - container should be extremely well documented to circumvent issues arising
* Takeaways
    - Documentation of containers (Formal & within Dockerfile) is crucial
    - Emphasys on good API design and reusability
---
### Chapter 2. : Ambassador Pattern
Definition: The ambassador pattern is essentially an `interfacing` container that connects the client container or any form of containers to external service. It inherently abstracts away the actuall implementation logic used to adequately provide connections to external services.
* Examples
    - Sharding: Imagine providing a sharded cache. A proxy container (Twemproxy) can be used to proxy client side requests to the proper redis cache server and the client has no knowledge of the actual logic utilized to effectively proxy. Similar example is seen in database sharding
    - Load Balancer: Easy to see how this is adheres to the ambassador pattern
    - Request Splitting: Image having implemented a new service and wanting to effectively test is stability given some production load. An Nginx proxy container could spun up to route 10% of production traffic to new service and efficiently test its performance. Again this implementation is agnostic to the client server.

* Takeways
    - Tradeoffs are always key & prevalent
---
### Chapter 3. : Adapter Pattern
Definition: The Adapter pattern is used to modify the interface of the application container so as to help it conform to some predefined interface expected for all applications.
* Examples:
    - Monitoring/Logging: In distributed systems, at times various containers run various languages and frameworks which all have their own logging formats. Now, these various loggin formats must be normalized in order to be adequately ingested by log metrics service like kibana. Additionally, some containers my not be able to be monitored by some central monitoring agent of the correct interface is not exported. Adapter containers that implement various interfaces are key to solving this problem efficiently.
    - Health Monitoring: Sometimes, teams may want to provide a richer set of monitoring functionalities to different services. Now, instead of updating each respective image, its much more efficient to add an adapter container. For example, if we want to perform health checking on a MYSQL database, instead of adding a health check to the service that interfaces with that database, we could create a container comprised of a shell script that queries/calls the container in order to check if the container is actually still up. 
* Notes
    - All this is performed by pulling a given container and an adapter container in a kubernetes pod. 

---
### Chapter 5.: Microservices
Definition: Microservices are individual services creating a context bound between different aspects of an application. They seperate areas of concerns helping teams be more autonomous and also providing for a more speedy development lifecycle.
* Notes
    - Added complexity is added expecially when debugging such distributed systems as well as enforcing fault tolerance.


