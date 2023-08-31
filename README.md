# Multi-container environment for deploying Spark, Kafka, Trino and Jupyter using Docker

This is a Docker multi-container environment with Spark, Kafka, Trino and Jupyter Notebook which can be easily deployed and installed.


## Docker installation




## Quick Start

To deploy and start the different containers, run:

```
  docker compose up -d
```

`docker compose` creates a docker network (and a Spark network) that can be found by running `docker network ls`.


## Spark

We are using the containers created by sdesilva26, more info about them can be found <a href="https://github.com/sdesilva26/docker-spark/blob/master/TUTORIAL.md">here</a>.

To use Spark, we enter into the container used to submit changes to our worker.

```
  docker exec -it spark-submit bash
```

From within the container we can jump into a scala shell using

```
  $SPARK_HOME/bin/spark-shell --conf spark.executor.memory=1G --conf spark.executor.cores=1 --master spark://spark-master:7077
```

Of course, you can change the memory and cores depending on your machine.

You can now run any jobs you want and they will appear in <a href="http://localhost:4040">http://localhost:4040</a> at the interface.

To exit the shell we can press CTRL+C and to exit the bash we just write `exit`.


## Trino

In order to use the Trino CLI is enough with executing the command:

```
  docker exec -it trino trino
```

To exit the CLI, just write `exit`
