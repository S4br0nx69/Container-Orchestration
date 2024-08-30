![image](https://github.com/user-attachments/assets/d4e4f752-edb7-41be-9712-b363245720bb)

### Main Objective : ###

I need to deploy a web poll application on a multi-host cluster using Kubernetes. The application consists of several containerized components and uses Traefik as a reverse proxy and load balancer.

### Application Components : ###
- Poll: A Python (Flask) web application that collects user votes and sends them to a Redis queue.
- Redis: An in-memory database that temporarily stores the votes waiting to be processed.
- Worker: A Java application that consumes the votes from Redis and stores them in a PostgreSQL database.
- PostgreSQL: A relational database that persistently stores the votes.
- Result: A Node.js web application that retrieves the votes from the database and displays the results.

### Requirement : ###
- I must configure a load balancer (Traefik) to handle the routing of the Poll and Result services.
- Two databases need to be configured: Redis and PostgreSQL, each with specific configurations.
- Three services need to be deployed and managed, two of which will be routed via Traefik.
- A monitoring tool (cadvisor) must be set up to monitor the containers.

### Deployment : ###
- The deployment involves creating and configuring several YAML files to orchestrate the different components of the application.
- Instructions are provided for deploying each component of the application in Kubernetes, as well as for configuring routing rules and persistent volumes.


