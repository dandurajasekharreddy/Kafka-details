
I**Install and run kafka using kraft on Windows  kraft || kafka in windows**
**Update properties files for logs as below:**
![image](https://github.com/user-attachments/assets/d5e1c57a-c5d4-4f62-a746-a1ed9123f239)

![image](https://github.com/user-attachments/assets/700d2015-3e6b-498e-bd97-0864208bd8c2)
![image](https://github.com/user-attachments/assets/c42b1ff1-356f-478c-b016-9ade1cd19747)

Set class path in envirnment variables.

**Required Commands:**

.\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties

.\bin\windows\kafka-server-start.bat .\config\server.properties

kafka-topics.bat --create --bootstrap-server localhost:9092 --replication-factor 1 --partition 1 --topic test

kafka-console-producer.bat --broker-list localhost:9092 --topic test
-------------------------------------------------------------------------------------------------------
Sample Data:

{"Name: "John", "Age":"31", "Gender":"Male"}
{"Name: "Emma", "Age":"27", "Gender":"Female"}
{"Name: "Ronald", "Age":"17", "Gender":"Male"}
---------------------------------------------------------------------------------------------------------

kafka-console-consumer.bat --topic test --bootstrap-server localhost:9092 --from-beginning

.\bin\windows\zookeeper-server-stop.bat .\config\zookeeper.properties

.\bin\windows\kafka-server-stop.bat .\config\server.properties



**Useful commands for Kraft :-** 

**TO generate UUID:-**

kafka-storage.bat random-uuid

**To set UUID to a variable :-**

set KAFKA_CLUSTER_ID={use the uuid generated above}
set KAFKA_CLUSTER_ID=E9Bu8rzBQAa01FuZUlyG8A 

**To format  log directories**

kafka-storage.bat format -t %KAFKA_CLUSTER_ID% -c ../../config/kraft/server.properties

**To start kafka server**

kafka-server-start.bat ../../config/kraft/server.properties

**To create topic**
kafka-topics.bat --create --topic first-kraft-topic --bootstrap-server localhost:9092

**To produce message on topic**
kafka-console-producer.bat --topic first-kraft-topic --bootstrap-server localhost:9092

**To produce message on topic using json file**
type C:\Users\hp\Downloads\sample.json | kafka-console-producer.bat --topic first-kraft-topic --bootstrap-server localhost:9092

**To consume message on topic**
kafka-console-consumer.bat --topic first-kraft-topic --from-beginning --bootstrap-server localhost:9092

---------------------------------------------------------------
**Open Source Kafka Startup in local**
--------------------------------------------------------------
**Start Zookeeper Server**

sh bin/zookeeper-server-start.sh config/zookeeper.properties

**Start Kafka Server / Broker**

sh bin/kafka-server-start.sh config/server.properties

**Create topic**

sh bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic NewTopic --partitions 3 --replication-factor 1

**list out all topic names**

sh bin/kafka-topics.sh --bootstrap-server localhost:9092 --list

**Describe topics**

sh bin/kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic NewTopic

**Produce message**

sh bin/kafka-console-producer.sh --broker-list localhost:9092 --topic NewTopic

**consume message**

sh bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic NewTopic --from-beginning

**Confluent Kafka Community Edition in local**
----------------------------------------------
**Start Zookeeper Server**

bin/zookeeper-server-start etc/kafka/zookeeper.properties

**Start Kafka Server / Broker**

bin/kafka-server-start etc/kafka/server.properties

**Create topic**

bin/kafka-topics --bootstrap-server localhost:9092 --create --topic NewTopic1 --partitions 3 --replication-factor 1

**list out all topic names**

bin/kafka-topics --bootstrap-server localhost:9092 --list

**Describe topics**

bin/kafka-topics --bootstrap-server localhost:9092 --describe --topic NewTopic1

**Produce message**

bin/kafka-console-producer --broker-list localhost:9092 --topic NewTopic1

**consume message**

bin/kafka-console-consumer --bootstrap-server localhost:9092 --topic NewTopic1 --from-beginning 

**Send CSV File data to kafka**

bin/kafka-console-producer --broker-list localhost:9092 --topic NewTopic1 <bin/customers.csv

**Decode log from tmp cluster metadata**
![image](https://github.com/user-attachments/assets/8c4f5885-8ee9-4e1c-af0f-8cdc221e8661)

 kafka-dump-log.bat --cluster-metadata-decoder --files ../00000000000000000000.log --print-data-log

 **Check the cluster status**

 kafka-metadata-quorum.bat --bootstrap-server localhost:9092 describe --status
