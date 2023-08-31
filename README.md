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

To use Spark, you need to enter into the container used to submit changes to our worker.

```
  docker exec -it spark-submit bash
```

From within the container you can jump into a scala shell using

```
  $SPARK_HOME/bin/spark-shell --conf spark.executor.memory=1G --conf spark.executor.cores=1 --master spark://spark-master:7077
```

Of course, you can change the memory and cores depending on your machine.

You can now run any jobs you want and they will appear in <a href="http://localhost:4040">http://localhost:4040</a> at the interface:

![image](https://github.com/Braisrg5/Spark-Kafka-Trino-Jupyter-Docker/assets/46173493/d486d04e-0f20-4565-84e2-492837c685aa)


To exit the shell you can press CTRL+C and to exit the bash you just have to write `exit`.


## Jupyter

After doing the compose command, if you want to use Jupyter you need to get into the logs of the container:

```
  docker logs jupyter
```

Once you do it, in one of the last lines you will see something like this:

![image](https://github.com/Braisrg5/Spark-Kafka-Trino-Jupyter-Docker/assets/46173493/a89916f7-6ce9-4583-90d0-3ad1b9a0d80b)

Just CTRL+click one of the links and you will be sent to jupyter lab.


## Trino

In order to use the Trino CLI is enough with executing the command:

```
  docker exec -it trino trino
```

To exit the CLI, just write `exit`
