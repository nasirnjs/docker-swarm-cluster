# Mastering Docker Swarm & Simplifying Container Orchestration
Table Of Content:
- [Mastering Docker Swarm \& Simplifying Container Orchestration](#mastering-docker-swarm--simplifying-container-orchestration)
  - [1. What is Docker?](#1-what-is-docker)
  - [2. What is Docker daemon?](#2-what-is-docker-daemon)
  - [3. Docker architecture](#3-docker-architecture)
  - [4. Kubernetes VS Docker Swarm](#4-kubernetes-vs-docker-swarm)
  - [5. What Is Docker Swarm?](#5-what-is-docker-swarm)
  - [6. How Does Docker Swarm Work?](#6-how-does-docker-swarm-work)
  - [7. Docker Swarm Cluster Setup](#7-docker-swarm-cluster-setup)
  - [8. Deploy Your Service on Docker Swarm](#8-deploy-your-service-on-docker-swarm)

In the fast-paced world of application development, efficiency is key. Docker revolutionized the scene by offering lightweight containerization as an alternative to cumbersome virtual machines (VMs).

Now, with Docker Swarm, managing clusters of Docker hosts is a breeze. This orchestration tool simplifies deployment and scaling, freeing developers from infrastructure complexities.

In this article, we'll explore Docker Swarm's architecture and practical usage. But first, let's grasp the basics of Docker containerization and its significance in modern development.

## 1. What is Docker?
Docker is a platform for developing, packaging & running applications in containers, providing a consistent and portable environment across different systems.\
It uses operating-system-level virtualization to deliver software in packages called containers

## 2. What is Docker daemon?
Docker daemon runs on the host operating system. It is responsible for running containers to manage docker services. 

## 3. Docker architecture
Docker follows Client-Server architecture, which includes the three main components that are Docker Client, Docker Host, and Docker Registry.

Docker Client: The user interface for interacting with Docker through commands or an API.

Docker Daemon (Host): A background process managing containers on the host machine.

Docker Registry: Repositories storing and distributing Docker images, like Docker Hub.

<p align="center">
  <img src="./image/high-level-overview-of-docker-architecture.png" alt="Docker Architecture" width="600" height="300"/>
</p>

## 4. Kubernetes VS Docker Swarm

Modern businesses are relying on containerization technologies to simplify the process of deploying and managing complex applications.Here's a comparison between Kubernetes and Docker Swarm.

<p align="center">
  <img src="./image/docker-swram-k8s.png" alt="Docker swram vs K8s" width="500" height="300"/>
</p>

| Feature                 | Kubernetes                                     | Docker Swarm                                      |
|-------------------------|------------------------------------------------|---------------------------------------------------|
| **Orchestration**       | Advanced orchestration capabilities.           | Simplified orchestration.                         |
| **Scaling**             | Horizontal and vertical scaling of containers.  | Horizontal scaling of services.                   |
| **High Availability**   | Built-in high availability features.           | High availability with automatic failover.        |
| **Networking**          | Advanced networking features.                  | Basic networking with overlay networks.           |
| **Load Balancing**      | Robust built-in load balancing.                | Basic load balancing capabilities.                |
| **Service Discovery**   | Integrated service discovery mechanisms.       | Service discovery using DNS or user-defined names.|
| **Storage Orchestration** | Support for persistent storage.              | Limited support for storage orchestration.        |
| **Security**            | Rich set of security features and policies.    | Basic security features with TLS encryption.      |
| **Community Support**   | Large and active community.                    | Active community support but smaller than Kubernetes.|
| **Ease of Use**         | Steeper learning curve, more complex setup.    | Simpler setup and easier to get started with.      |
| **Resource Utilization** | Efficient resource utilization.                | Efficient resource utilization.                   |
| **Popularity**          | Widely adopted by enterprises and cloud providers. | Gaining popularity, but not as widely adopted as Kubernetes. |
| **Ecosystem**           | Rich ecosystem with extensive tools and integrations. | Growing ecosystem with fewer tools and integrations compared to Kubernetes. |

## 5. What Is Docker Swarm?

Docker Swarm is a container orchestration tool that allows you to manage a cluster of Docker hosts and deploy and scale containerized applications seamlessly. It forms a part of the Docker ecosystem and simplifies the management of containerized environments, making it easier for developers and operators to deploy and maintain applications at scale.

**Key Features of Docker Swarm:**
1. Orchestration: Docker Swarm automates the deployment, scaling, and management of containerized applications across a cluster of Docker hosts.

2. High Availability: It ensures high availability by distributing containerized applications across multiple nodes in the cluster, allowing for failover and redundancy.

3. Scalability: Docker Swarm enables horizontal scaling of applications by adding or removing containers based on workload demands, ensuring optimal resource utilization.

4. Load Balancing: It includes built-in load balancing capabilities to evenly distribute incoming traffic across containers running on different nodes in the cluster.

5. Security: Docker Swarm provides security features such as mutual TLS authentication and encryption to secure communication between nodes and containers within the cluster.

6. Ease of Use: With a simple and intuitive command-line interface, Docker Swarm is easy to set up and use, making it accessible to both developers and operators.


## 6. How Does Docker Swarm Work?

Docker Swarm works by orchestrating a cluster of Docker hosts, enabling users to deploy and manage containerized applications across multiple nodes seamlessly. Here's an overview of how Docker Swarm operates:

1. Initialization: To create a Docker Swarm cluster, one of the Docker hosts is designated as the manager node. This node initializes the Swarm, forming the control plane responsible for managing the cluster.

2. Joining Nodes: Additional Docker hosts can join the Swarm as either manager or worker nodes. Manager nodes handle cluster management tasks, while worker nodes execute the containerized applications.

3. Service Deployment: Users define services, which represent containerized applications along with their configurations and desired states. These services are deployed to the Swarm using Docker commands or Docker Compose files.

4. Task Scheduling: The manager node schedules tasks, which represent individual instances of services, across the worker nodes in the Swarm. Tasks are distributed based on resource availability and constraints specified by the user.

5. Load Balancing: Docker Swarm includes built-in load balancing mechanisms to evenly distribute incoming traffic among the tasks running on different nodes. This ensures optimal utilization of resources and high availability of applications.

6. Scaling: Users can scale services horizontally by adjusting the number of replicas, which determines the number of tasks running for a particular service. Docker Swarm automatically distributes these tasks across available nodes.

7. Health Monitoring: Docker Swarm continuously monitors the health of services and individual tasks within the cluster. If a task or node becomes unhealthy, Docker Swarm takes corrective actions, such as restarting tasks or rescheduling them to healthy nodes.

8. Networking: Docker Swarm provides networking features that enable communication between containers running on different nodes in the cluster. This allows for seamless interaction between services and ensures connectivity within the application architecture.

9. Security: Docker Swarm offers security features such as mutual TLS authentication, encryption of network traffic, and role-based access control (RBAC) to protect the cluster and its resources from unauthorized access and malicious activities.

<p align="center">
  <img src="./image/docker-swarm-architecture.png" alt="Docker Swarm Architecture" width="600" height="400"/>
</p>


## 7. Docker Swarm Cluster Setup

Setting up your first Docker Swarm Demo can indeed be a rewarding experience, showcasing the capabilities of containerized applications. To help you get started, here are the steps to set up your first Docker Swarm Demo.

**Basic Prerequisites for Setting Up Docker Swarm**

1. Docker Installed: Ensure Docker Engine is installed on all nodes.
2. Multiple Nodes: Need multiple machines for the Swarm cluster.
3. Network Connectivity: Nodes must communicate with each other.
4. Static IPs or Hostnames: Nodes need identifiable addresses.
5. Open Ports: Ports 2377, 7946, and 4789 should be open.
6. Consistent Docker Versions: Use the same Docker version on all nodes.
7. Sufficient Resources: Nodes should have enough CPU, memory, and disk space.

**7.1 Install Docker from [Here](https://docs.docker.com/engine/install/ubuntu/)**

**7.2 Initializing a Swarm [Reference](https://docs.docker.com/engine/swarm/)**

Initialize Swarm.\
`docker swarm init`

Initialize Swarm with specific address.\
`docker swarm init --advertise-addr <MANAGER-IP>`

Generate tocken for node join as manager.\
`docker swarm join-token manager`

Generate tocken for node join as worker.\
`docker swarm join-token worker`

Forcely advertise a cluster.\
`docker swarm init --force-new-cluster --advertise-addr <MANAGER-IP>`

**7.3 Joining Nodes to Swarm**

Join as a worker.\
`docker swarm join --token <TOKEN> <MANAGER-IP>:<PORT>`

**7.4 Managing Nodes**

List Nodes\
`docker node ls`

Inspect Node\
`docker node inspect <NODE-ID>`

Promote Node to Manager, this CMD from master node\
`docker node promote <NODE-ID>`

Demote Manager to Worker\
`docker node demote <NODE-ID>`

Remove Node from Swarm\
`docker node rm <NODE-ID>`

Node itself Leave from cluster.\
`docker swarm leave`

Node to "drain" availability, it means that the node is being taken out of service gracefully.\
`docker node update --availability=drain node1`

Setting a node's availability to "active" means that the node is available to receive new tasks and services.\
`docker node update --availability=active node1`

To get the existing Docker Swarm manager join token.\
`docker swarm join-token manager`

## 8. Deploy Your Service on Docker Swarm

To add replicas to the Docker Swarm service with replicas.\
`docker service create --name nginx --publish 80:80 --replicas 3 nginx`

To list the services in a Docker Swarm cluster.\
`docker service ls`

To update the number of replicas for a Docker Swarm service.\
`docker service update --replicas 5 nginx`

To delete the "nginx" service in Docker Swarm.\
`docker service rm nginx`

To see Service Logs.\
`sudo docker service logs nginx -f`

---


[References for Update](https://www.simplilearn.com/tutorials/docker-tutorial/docker-swarm)
