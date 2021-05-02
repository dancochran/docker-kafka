```
docker exec -it 6661831e513e bash

kafka-verifiable-producer --broker-list kafka-1:9092 --max-messages 1000 --repeating-keys 10 --topic test.test
kafka-verifiable-consumer --broker-list kafka-1:9092 --topic test.test --group-id test-1

kafka-topics --zookeeper zookeeper-1:2181 --list
kafka-topics --zookeeper zookeeper-1:2181 --describe --topic test.test

kafka-topics --create --topic fs-cli-test --bootstrap-server localhost:9092
    --config cleanup.policy=delete
kafka-topics --describe --topic fs-cli-test --bootstrap-server localhost:9092

kafka-topics --alter --topic fs-cli-test --zookeeper zookeeper-1:2181 --config cleanup.policy=delete
# cleanup.policy=compact is for compacted topics, both can be used together; compacted enforces valid keys

kafka-console-producer --topic fs-cli-test --bootstrap-server localhost:9092
kafka-console-consumer --topic fs-cli-test --bootstrap-server localhost:9092 
