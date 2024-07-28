
I**Install and run kafka using kraft on Windows  kraft || kafka in windows**

Useful commands :- 

**TO generate UUID:-**
kafka-storage.bat random-uuid

**To set UUID to a variable :-**
set KAFKA_CLUSTER_ID={use the uuid generated above}

**To format  log directories**
kafka-storage.bat format -t %KAFKA_CLUSTER_ID% -c ../../config/kraft/server.properties

**To start kafka server**
kafka-server-start.bat ../../config/kraft/server.properties

**To create topic**
kafka-topics.bat --create --topic first-kraft-topic --bootstrap-server localhost:9092

**To produce message on topic**
kafka-console-producer.bat --topic first-kraft-topic --bootstrap-server localhost:9092

**To consume message on topic**
kafka-console-consumer.bat --topic first-kraft-topic --from-beginning --bootstrap-server localhost:9092
