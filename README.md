# Multi-container environment for deploying Spark, Kafka, Trino and Jupyter using Docker

This is a Docker multi-container environment with Spark, Kafka, Trino and Jupyter Notebook which can be easily deployed and installed.


## Docker installation
### Set up the apt repository

Firstly, update the `apt` package index and install packages to allow `apt` to use a repository over HTTPS:

```
  sudo apt-get update
  sudo apt-get install ca-certificates curl gnupg
```

Add Docker's official GPG key:

```
  sudo install -m 0755 -d /etc/apt/keyrings
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
  sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

Use the following command to set up the repository

```
  echo \ "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \ "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

And finally, update again the `apt` package index:

```
  sudo apt-get update
```
### Install Docker Engine

To install the latest version, run:
```
  sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Verify that the Docker Engine installation is succesful by running the `hello-world` image:
```
  sudo docker run hello-world
```
### Manage Docker as a non-root user

Create the `docker` group

```
  sudo groupadd docker
```

Add your user to the `docker` group
```
  sudo usermod -aG docker $USER
```

Run the following command to activate the changes to groups;
```
  newgrp docker
```

Verify that you can run `docker` commands without `sudo`.
```
  docker run hello-world
```


## Quick Start

Download the compose.yml file, and save it in your working environment. To pull and start the different containers, run:

```
  docker compose up -d
```

The different images will be downloaded from the Docker Hub, installed on your machine and started.

`docker compose` creates a docker network (and a Spark network) that can be found by running `docker network ls`.

When you are finished, run `docker compose down` to stop and remove all the containers.


## Spark

We are using the containers created by sdesilva26, more info about them <a href="https://github.com/sdesilva26/docker-spark/blob/master/TUTORIAL.md">here</a>.

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


## Kafka

We are using the Kafka containers created by Confluent, more info about them <a href="https://docs.confluent.io/platform/current/installation/docker/installation.html">here</a>.

To connect to kafka, get into the container's bash
```
  docker exec -it kafka bash
```

From here you can use the usual kafka commands such as `kafka-topics`. The server you need to connect to is `localhost:29092`.

Here is an example where we create a topic called "foo" and send it a "Hello world":ç
![image](https://github.com/Braisrg5/Spark-Kafka-Trino-Jupyter-Docker/assets/46173493/717034eb-17e5-444c-a7c3-992c2c146f7d)

To exit the container, just write `exit`.


## Jupyter

We are using the official Jupyter containers, more info about them can be found <a href="https://jupyter-docker-stacks.readthedocs.io/en/latest/">here</a>.

After doing the compose command, to connect to Jupyter you need to wait for a bit (so the program sets up completely) and then get into the logs of the container:
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
