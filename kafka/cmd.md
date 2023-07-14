## 查看topic列表
kafka-topics.sh --bootstrap-server localhost:9092 --list

## 创建topic
kafka-topics.sh --bootstrap-server localhost:9092 --create --topic TMALL_WEBHOOK_DATA --partitions 1 --replication-factor 1 --config max.message.bytes=64000 --config flush.messages=1

## 查看topic信息
kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic my-topic

## 发送消息到topic
kafka-console-producer.sh --broker-list localhost:9092 --topic my-topic