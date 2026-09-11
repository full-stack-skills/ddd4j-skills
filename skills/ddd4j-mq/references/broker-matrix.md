# Broker 矩阵

当前模块包括 activemq、disruptor、kafka、mqtt、mqtt-mica、nats、ons、pulsar、rabbitmq、redis-stream、rocketmq、sqs、tdmq、spring。

每个实现必须核对 Properties、MQClient、Acknowledgment、header 映射和测试；Artemis 若仅通过 ActiveMQ/JMS 兼容或上层依赖出现，要明确当前是否有独立 adapter。
