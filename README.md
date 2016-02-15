<h1>Kafka Availability Monitor </h1>

Kafka Availability monitor allows you to monitor the end to end availability and latency for sending and reading data from Kafka.
Producer Availability is defined as (Number of successful message sends accross all Topics and Partitions)/(Number of message send attempts)
Consumer Availability is defined as (Number of successfull tail data reads accross all Topics and Partitions)/(Number of message send attempts)

## Usage
1. Clone the repository locally
Git clone

2. Change the resource file(s)
KafkaAvailability / src / main / resources / metadatamanagerProperties.json and add your zookeeperhost ip and ports
```
"zooKeeperHosts": "1.1.1.1:2181,2.2.2.2:2181",
```
KafkaAvailability / src / main / resources / log4j.properties
KafkaAvailability / src / main / resources / appProperties.json
3. If using precompiled jar, inject the modified resource file into the jar:
```
jar uf KafkaAvailability-1.0-SNAPSHOT-jar-with-dependencies.jar metadatamanagerProperties.json
```
If assembling jar from source, if you want to report metrics to MS SQL Server, you must download and install the jdbc driver into your maven repo:
Visit the MSDN site for SQL Server and download the latest version of the JDBC driver for your operating system.
Unzip the package
Open a command prompt and switch into the expanded directory where the jar file is located.
Execute the following command. Be sure to modify the jar file name and version as necessary:
```
mvn install:install-file -Dfile=sqljdbc4.jar -Dpackaging=jar -DgroupId=com.microsoft.sqlserver -DartifactId=sqljdbc4 -Dversion=4.0
```
Finally, assemble jar using maven:
```
mvn clean compile assembly:single
```
4. Run the assembled jar like this:
```
java.exe -jar KafkaAvailability-1.0-SNAPSHOT-jar-with-dependencies.jar -c ClusterName
```
5. If you want to report metrics to SQL Server, put the connection string in 
KafkaAvailability / src / main / resources / AppProperties.json


## Other Documentation

Please refer to JavaDoc for detailed code documentation.

## License

[![License](https://img.shields.io/badge/license-MIT-blue.svg?style=plastic)](https://github.com/Microsoft/Kafka-Availability-Monitor/blob/master/LICENSE.txt)

Kafka Availability Monitor is licensed under the MIT license. See [LICENSE](LICENSE) file for full license information.