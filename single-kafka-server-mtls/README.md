
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
./bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --consumer.config config/consumer.properties
```


## Producer
```
./bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic test --producer.config config/producer.properties
```


In caso di autenticazione fallita: 

```
[2021-05-04 08:43:28,764] ERROR [Consumer clientId=consumer-test-consumer-group-1, groupId=test-consumer-group] Connection to node -1 (localhost/127.0.0.1:9092) failed authentication due to: SSL handshake failed (org.apache.kafka.clients.NetworkClient)
[2021-05-04 08:43:28,765] WARN [Consumer clientId=consumer-test-consumer-group-1, groupId=test-consumer-group] Bootstrap broker localhost:9092 (id: -1 rack: null) disconnected (org.apache.kafka.clients.NetworkClient)
[2021-05-04 08:43:28,782] ERROR Error processing message, terminating consumer process:  (kafka.tools.ConsoleConsumer$)
org.apache.kafka.common.errors.SslAuthenticationException: SSL handshake failed
Caused by: javax.net.ssl.SSLProtocolException: Unexpected handshake message: server_hello
```