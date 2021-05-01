---
title: Message Queue
date: 2020-07-03 20:12:27
tags:
---

> “Should I use RabbitMQ or Kafka?” For some reason, many developers view these technologies as interchangeable. While this is true for some cases, there are various underlying differences between these platforms.

> As a result, different scenarios require a different solution, and choosing the wrong one might severely impact your ability to design, develop, and maintain your software solution.


## Asynchronous Messaging Patterns

Asynchronous messaging is a messaging scheme where message production by a producer is decoupled from its processing by a consumer. When dealing with messaging systems, we typically identify two main messaging patterns — message queuing and publish/subscribe.

### Message queueing 

In the message-queuing communication pattern, queues temporally decouple producers from consumers. Multiple producers can send messages to the same queue; however, when a consumer processes a message, it’s locked or removed from the queue and is no longer available. Only a single consumer consumes a specific message.
![image](https://miro.medium.com/max/1400/1*sKXP4QfrwFCGZy1fKZ_FnA.png)

As a side note, if the consumer fails to process a certain message, the messaging platform typically returns the message to the queue where it’s made available for other consumers. Besides temporal decoupling, queues allow us to scale producers and consumers independently as well as providing a degree of fault-tolerance against processing errors.

### Publish/subscribe

In the publish/subscribe (or pub/sub) communication pattern, a single message can be received and processed by multiple subscribers concurrently.

![image](https://miro.medium.com/max/1400/1*Q1Ou71PmWgiqP7KeMyhajw.png)

## RabbitMQ vs Kafka vs ActiveMQ: What are the differences?

RabbitMQ, Kafka, and ActiveMQ are all messaging technologies used to provide asynchronous communication and decouple processes (detaching the sender and receiver of a message). They are called message queues, message brokers, or messaging tools. RabbitMQ, Kafka, and ActiveMQ all serve the same basic purpose, but can go about their jobs differently. Kafka is a high-throughput distributed messaging system. RabbitMQ is an AMQP based reliable message broker. ActiveMQ and Kafka are both Apache products, and both written in Java; RabbitMQ is written in Erlang.

##### More Info about Kafka
https://github.com/Snailclimb/springboot-kafka/blob/master/docs/1-大白话带你认识Kafka.md

##### More Info about RabitMQ
https://github.com/Snailclimb/JavaGuide/blob/master/docs/system-design/data-communication/rabbitmq.md