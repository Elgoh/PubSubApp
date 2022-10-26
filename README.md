# docker-kafka-cluster

docker-kafka-cluster allows to deploy a kafka multi node cluster (3 brokers, 1 zookeeper) with docker.

Unable to follow the guide in OTOT pdf thus I used 1 zookeeper instead.
Better to learn from a working code than none at all.

Referenced from: https://medium.com/@PierreKieffer/deploy-a-kafka-multi-node-cluster-with-docker-72878ddbaf96

~ Special thanks to @PierreKieffer for the guide ~

## Download Docker

- Install docker engine and docker-compose from: https://docs.docker.com/get-docker/

## Build the base image

- clone the repo
- `docker build -t kafka_base .`

## Launch the kafka cluster in docker

- `docker-compose up`

## Test

### 1. Run a client

- `docker run -it --network host kafka_base /bin/bash`

### 2. Create a topic

- `./bin/kafka-topics --create --zookeeper localhost:2181 --replication-factor 3 --partitions 3 --topic TOPIC_NAME`

### 3. Run a console producer/publisher

- Open a new terminal for publisher
- `docker run -it --network host kafka_base /bin/bash`
- `./bin/kafka-console-producer --broker-list localhost:9091,localhost:9092,localhost:9093 --topic TOPIC_NAME`

### 4. Run a console Consumer/Subscriber

- Open a new terminal for Subcriber
- `docker run -it --network host kafka_base /bin/bash`
- `./bin/kafka-console-consumer --topic TOPIC_NAME --bootstrap-server localhost:9091,localhost:9092,localhost:9093`

### Monitor Kafka Cluster

- Either view it in docker desktop or
- Use a new terminal and run `docker ps`

### To run multiple Publishers/Subscribers/Topics

- Open up new terminal
- Run either steps: 2, 3, 4 with the correct TOPIC_NAME
