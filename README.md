### Main Objective : ###
I need to deploy a web poll application on a multi-host cluster using Kubernetes. The application consists of several containerized components and uses Traefik as a reverse proxy and load balancer.

### Application Components : ###
- Poll: A Python (Flask) web application that collects user votes and sends them to a Redis queue.
- Redis: An in-memory database that temporarily stores the votes waiting to be processed.
- Worker: A Java application that consumes the votes from Redis and stores them in a PostgreSQL database.
- PostgreSQL: A relational database that persistently stores the votes.
- Result: A Node.js web application that retrieves the votes from the database and displays the results.

### Requirement : ###


