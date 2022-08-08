# Kafka-Practice

## Building the Kafka image using the dockerfile

`docker build . -t kafka-practice:3.2.1`

---

## Copying the properties for the server and zookeeper from image to locally so we can mount it while building

`docker cp kafka:/kafka/config/server.properties ./server.properties` <br>
`docker cp kafka:/kafka/config/zookeeper.properties ./zookeeper.properties`

---

## Build a zookeeper instance

`docker build . -t zookeeper-practice:3.2.1`

---

## Create a network instance for kafka

`docker network create kafka`

---

## Run the zookeeper instance

`docker run -d --rm --name zookeeper-1 --net kafka -v ${PWD}/config/zookeeper-1/zookeeper.properties:/kafka/config/zookeeper.properties zookeeper-practice:3.2.1` <br>
To check the logs: `docker logs zookeeper-1`

---

## Run the kafka instance

1. `docker run -d --rm --name kafka-1 --net kafka -v ${PWD}/config/kafka-1/server.properties:/kafka/config/server.properties kafka-practice:3.2.1`

2. `docker run -d --rm --name kafka-2 --net kafka -v ${PWD}/config/kafka-2/server.properties:/kafka/config/server.properties kafka-practice:3.2.1`

3. `docker run -d --rm --name kafka-3 --net kafka -v ${PWD}/config/kafka-3/server.properties:/kafka/config/server.properties kafka-practice:3.2.1` <br>

To check the logs: `docker logs kafka-{number}`

---

## Creating a Topic

Enter the zookeeper container: `docker exec -it zookeeper-1 bash`

---
