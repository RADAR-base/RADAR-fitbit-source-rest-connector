Kafka Connect REST Fitbit connector
===

This repository will be merged with updated Fitbit REST logic in the next release.


Building and running Fitbit example
---

    mvn clean install
    cd fitbit/fitbit-rest-service
    mvn clean install
    cd ..
    docker-compose up -d

    docker exec -it spring_connect_1 bash -c \
     "kafka-topics --zookeeper zookeeper \
       --topic restSourceDestinationTopic --create \
       --replication-factor 1 --partitions 1"

Pull history of activity 

    curl -X POST \
       -H 'Host: connect.example.com' \
       -H 'Accept: application/json' \
       -H 'Content-Type: application/json' \
      http://localhost:8083/connectors -d @config/activity_history.json

Change CONNECT_VALUE_CONVERTER in the docker-compose.yml to org.apache.kafka.connect.storage.StringConverter if you don't want to use Avro.

    docker exec -it spring_connect_1 bash -c \
     "kafka-avro-console-consumer --bootstrap-server kafka:9092 \
      --topic restSourceDestinationTopic --from-beginning \
      --property schema.registry.url=http://schema_registry:8081/"

    docker logs -f spring_webservice_1

    docker-compose down
    cd ../..

Change CONNECT_VALUE_CONVERTER in the docker-compose.yml
to org.apache.kafka.connect.storage.StringConverter if you don't want to use Avro.

    docker exec -it spring_connect_1 bash -c \
     "kafka-console-consumer --bootstrap-server kafka:9092 \
      --topic restSourceDestinationTopic --from-beginning"

