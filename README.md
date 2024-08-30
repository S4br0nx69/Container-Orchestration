# Kubernetes Container Orchestartion #

### Overview ###

The Kubernetes Container Orchestartion is a scalable and containerized web application orchestrated using Kubernetes. The project simulates a poll application with multiple interconnected services, managed by Kubernetes, and monitored for performance. Traefik is used as the load balancer and reverse proxy to efficiently route traffic between services.

### Project Components ###

- Poll (Flask Application) : A Python-based web application that collects user votes and pushes them to a Redis queue
- Redis Queue : An in-memory data store that temporarily holds the votes until they are processed
- Worker (Java Application) : A Java-based application that processes the votes from Redis and stores them in the PostgreSQL database
- PostgreSQL Database : A relational database that persistently stores the processed votes
- Result (Node.js Application) : A Node.js-based web application that retrieves and displays the poll results from the PostgreSQL database
- Traefik (Load Balancer) : Manages the routing of traffic between the services and provides an entry point to the application
- cAdvisor (Monitoring Tool) : A tool for monitoring the resource usage and performance of the containers


### Architecture ###

The architecture of this project is designed to ensure high availability, scalability, and efficient management of resources. Below is an overview of the key architectural components :
- Kubernetes Master Node : Orchestrates the entire cluster, managing deployments, scaling, and service discovery
- Kubernetes Worker Nodes : Host the actual application services. At least two nodes are used to ensure redundancy and high availability
- Traefik: Acts as the entry point for the application, balancing the load across the services and routing requests based on predefined rules

![Diagramme sans nom drawio (2)](https://github.com/user-attachments/assets/53511900-769f-41a2-af67-3bb973ba71ec)


### Prerequisites ###

Before you start deploying the application, ensure you have the following tools and environments set up : 
- Kubernetes Cluster: A cluster with at least one master node and two worker nodes
- kubectl : Kubernetes command-line tool
- Docker : For building and managing container images
- Traefik : Configured as the ingress controller for the Kubernetes cluster
- cAdvisor : For monitoring container resource usage


### Deployment Instructions ###

To deploy the application, follow these steps:











