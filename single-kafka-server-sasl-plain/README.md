

## Start the VM
```
vagrant up
```

Server logs should seem like this:
```
[2021-05-04 12:18:02,355] INFO Updated AUTHENTICATED max connection creation rate to 2147483647 (kafka.network.ConnectionQuotas)
[2021-05-04 12:18:02,359] INFO Awaiting socket connections on localhost:9092. (kafka.network.Acceptor)
[2021-05-04 12:18:02,382] INFO Successfully logged in. (org.apache.kafka.common.security.authenticator.AbstractLogin)
```

## Consumer 
```
./bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --consumer.config config/consumer.properties
```

## Producer
```
./bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic test --producer.config config/producer.properties
```

```
[2021-05-04 12:20:19,068] INFO [SocketServer brokerId=0] Failed authentication with /127.0.0.1 (Unexpected Kafka request of type METADATA during SASL handshake.) (org.apache.kafka.common.network.Selector)
```