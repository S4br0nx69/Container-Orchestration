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
- Traefik : Acts as the entry point for the application, balancing the load across the services and routing requests based on predefined rules

![Diagramme sans nom drawio (2)](https://github.com/user-attachments/assets/53511900-769f-41a2-af67-3bb973ba71ec)


### Prerequisites ###

Before you start deploying the application, ensure you have the following tools and environments set up : 
- Kubernetes Cluster: A cluster with at least one master node and two worker nodes
- kubectl : Kubernetes command-line tool
- Docker : For building and managing container images
- Traefik : Configured as the ingress controller for the Kubernetes cluster
- cAdvisor : For monitoring container resource usage


### Deployment Instructions ###

To deploy the application, follow these steps :
⚠️ Ensure your Kubernetes cluster is up and running with the necessary nodes.

#### 1 Deploy Services ####

- Deploy the PostgreSQL database :
```bash
kubectl apply -f postgres.secret.yaml -f postgres.configmap.yaml -f postgres.volume.yaml -f postgres.deployment.yaml -f postgres.service.yaml
```

- Deploy Redis :
```bash
kubectl apply -f redis.configmap.yaml -f redis.deployment.yaml -f redis.service.yaml
```

- Deploy the Poll, Worker, and Result services :
```bash
kubectl apply -f poll.deployment.yaml -f worker.deployment.yaml -f result.deployment.yaml -f poll.service.yaml -f result.service.yaml -f poll.ingress.yaml -f result.ingress.yaml
```

- Deploy Traefik :
```bash
kubectl apply -f traefik.rbac.yaml -f traefik.deployment.yaml -f traefik.service.yaml
```
#### 2 Initialize the Database ####

- Create the necessary tables in PostgreSQL :
```bash
echo "CREATE TABLE votes (id text PRIMARY KEY, vote text NOT NULL);" | kubectl exec -i -c postgres-container psql -U POSTGRES_USER
```

#### 3 Configure Hosts File ####

- Map the external IPs to the poll and result services :
```bash
echo "$(kubectl get nodes -o jsonpath='{.items[*].status.addresses[?(@.type=="ExternalIP")].address}') poll.dop.io result.dop.io" | sudo tee -a /etc/hosts
```

#### 4 Monitor the Application : 
- Use cAdvisor to monitor container performance :
```bash
kubectl apply -f cadvisor.daemonset.yaml
```
- The Traefik dashboard is running at http://localhost:30042 








