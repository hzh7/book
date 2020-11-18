# Kafka

## 概念

  - Kafka作为一个集群，运行在一台或者多台服务器上.
  - Kafka 通过 topic 对存储的流数据进行分类。
    - Topic 就是数据主题，是数据记录发布的地方,可以用来区分业务系统。Kafka中的Topics总是多订阅者模式，一个topic可以拥有一个或者多个消费者来订阅它的数据。
    - 对于每一个topic， Kafka集群都会维持一个分区日志
    - 消费者组中的消费者实例个数不能超过分区的数量
  - 每条记录中包含一个key，一个value和一个timestamp（时间戳）。


## kafka终端命令  
```
启动zk： bin/zookeeper-server-start.sh config/zookeeper.properties

启动kafka服务：bin/kafka-server-start.sh config/server.properties

kafka生产者：bin/kafka-console-producer.sh --broker-list localhost:9092 --topic topic

kafka消费者：bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic topic --from-beginning
```