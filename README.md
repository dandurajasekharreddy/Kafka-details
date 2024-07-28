
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
