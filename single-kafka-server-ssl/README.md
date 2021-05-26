
## Create certificates
```
cd certs 
make all
```

## Start the VM
```
vagrant up
```


## Consumer 
```
bootstrap.servers=localhost:9092

security.protocol=SSL
ssl.truststore.location: /etc/certs/kafka.client.truststore.jks
ssl.truststore.password: changeit

group.id=test-consumer-group
```

```
./bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --consumer.config config/consumer.properties
```


## Producer
```
bootstrap.servers=localhost:9092

security.protocol=SSL
ssl.truststore.location: /etc/certs/kafka.client.truststore.jks
ssl.truststore.password: changeit
```


```
./bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic test --producer.config config/producer.properties
```