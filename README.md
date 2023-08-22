# Multi-container environment for deploying Spark, Kafka, Trino and Jupyter using Docker

This is a Docker multi-container environment with Spark, Kafka, Trino and Jupyter Notebook which can be easily deployed and installed.


## Quick Start

To deploy and start the different containers, run:

```
  docker compose up -d
```

`docker-compose` creates a docker network that can be found by running `docker network list`.


## Trino

In order to use the Trino CLI is enough with executing the command:

```
  docker exec -it trino trino
```

To exit the CLI, just write `exit`
