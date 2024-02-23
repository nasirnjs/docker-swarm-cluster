# Manage Swarm Service Networks

This page describes networking for swarm services.

## Swarm and Types of Traffic

A Docker swarm generates two different kinds of traffic:

- **Control and Management Plane Traffic:** This includes swarm management messages, such as requests to join or leave the swarm. This traffic is always encrypted. Docker swram Certificate location `/var/lib/docker/swarm/certificates`

- **Application Data Plane Traffic:** This includes container traffic and traffic to and from external clients.


## Docker overlay network
A Docker overlay network is a type of network that allows containers running on different Docker hosts to communicate with each other securely and efficiently, regardless of the host they are running on. It's primarily used in Docker Swarm mode, which is Docker's native clustering and orchestration solution.

Here are some key features and characteristics of Docker overlay networks:

- Cross-host communication: Containers running on different Docker hosts can communicate with each other seamlessly as if they were on the same host.

- Overlay network: The overlay network operates on top of the existing network infrastructure and provides a virtual network that spans across multiple Docker hosts.

- Encrypted communication: Communication between containers on the overlay network can be encrypted to ensure security.

- Service discovery: Docker Swarm provides built-in service discovery mechanisms, which means containers can discover and communicate with each other using service names instead of IP addresses.

- Load balancing: Docker Swarm also includes load balancing capabilities, allowing traffic to be distributed evenly across containers within the overlay network.

- Scalability: Overlay networks are designed to be scalable, allowing for the addition of more Docker hosts and containers as needed without significant changes to the network configuration.


## Docker Swarm Ingress Traffic
The Docker Ingress network is a special overlay network created automatically by Docker Swarm when you initialize a Swarm cluster or deploy services in Docker Swarm mode. It is primarily used for routing external traffic into the Swarm services.

Here are some key points about the Docker Ingress network:

- Routing external traffic: The Ingress network allows incoming traffic from external sources, such as clients or users accessing your applications, to be routed into the Swarm services running inside the cluster.

- Load balancing: Ingress network provides built-in load balancing capabilities for distributing incoming traffic across multiple instances of a service. It ensures that requests are evenly distributed among the available replicas of a service.

- Service discovery: Docker Swarm's built-in DNS service automatically resolves the service names to the appropriate containers' IP addresses within the cluster. This enables seamless communication between the external clients and the services running in the Swarm cluster.

- Secure communication: Ingress network can be configured to use TLS encryption to secure the communication between the external clients and the services running in the Swarm cluster.

- Dynamic reconfiguration: Docker Swarm's routing mesh dynamically reconfigures itself as services scale up or down, ensuring that traffic is always directed to the available instances of the services.


## Use of Swarm Routing Mesh with Ingress

Docker Swarm's routing mesh utilizes the Ingress network to route incoming traffic to the appropriate services within the Swarm cluster. The routing mesh is a key feature of Docker Swarm that facilitates load balancing and service discovery.

### How it works:

1. **Ingress Network**: When you initialize a Docker Swarm cluster or deploy services in Swarm mode, Docker automatically creates an Ingress network. This network serves as the entry point for external traffic into the Swarm cluster.

2. **Routing Mesh**: The Swarm routing mesh is responsible for routing incoming traffic from external clients to the appropriate services running within the cluster. It dynamically configures itself to ensure that traffic is distributed evenly across all available instances of a service.

3. **Load Balancing**: The routing mesh provides built-in load balancing capabilities, ensuring that incoming requests are evenly distributed among the replicas of a service. This helps in optimizing the use of resources and improving the overall performance of the applications running in the Swarm cluster.

4. **Service Discovery**: Docker Swarm's built-in DNS service resolves service names to the appropriate containers' IP addresses within the cluster. This enables seamless communication between external clients and the services running in the Swarm cluster, facilitated by the routing mesh.

In summary, the Swarm routing mesh leverages the Ingress network to efficiently route incoming traffic to the services running in the Docker Swarm cluster, providing load balancing, service discovery, and dynamic reconfiguration capabilities.


[References](https://docs.docker.com/engine/swarm/networking/)
[Ref.routing-mesh](https://docs.docker.com/engine/swarm/ingress/)
