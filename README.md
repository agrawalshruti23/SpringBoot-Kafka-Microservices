Reference: https://www.youtube.com/watch?v=euKhMQRW3A8&list=PLGRDMO4rOGcOlnu6QhogZDNFFwiwKh5X9&index=1 

Spring Boot Kafka Microservices Project

Here's a high-level explanation of how Kafka could be implemented in such a project:

Base-Domain Service:

This service might act as the foundational service for your microservices architecture.
It may define common data models, shared libraries, and configurations that are used across multiple microservices.
Order Service:

The Order Service is responsible for managing and processing orders.
When an order is placed, updated, or canceled, it publishes events to a Kafka topic. These events represent significant actions in the order lifecycle.
Examples of events: "Order Placed," "Order Updated," "Order Canceled."
Stock Service:

The Stock Service manages inventory and product availability.
It subscribes to events from the Order Service via Kafka to keep track of changes in orders that may affect stock levels.
For example, when an "Order Placed" event is received, the Stock Service may reduce the available stock for the ordered products.
Email Service:

The Email Service handles sending order-related emails to customers.
It subscribes to events from the Order Service to trigger email notifications.
For instance, when an "Order Placed" event is received, the Email Service may send an order confirmation email.
Here's how Kafka fits into this architecture:

Event Publishing: When actions occur within the Order Service, such as placing an order, the service publishes events to a Kafka topic. These events are produced to the Kafka cluster.

Event Consumption: The Stock Service and Email Service subscribe to the relevant Kafka topics. They consume events from these topics to respond to changes in the system. This asynchronous communication allows for decoupling and scalability.

Event Sourcing: Kafka can serve as an event sourcing mechanism, where the state changes of entities (e.g., orders, stock) are captured as a sequence of immutable events. This allows for auditing, replaying events, and reconstructing the current state.

Fault Tolerance: Kafka's distributed nature ensures fault tolerance and scalability. Even if one service or component goes down, Kafka can replay events when the service recovers.




1. To start the zookeeper
cd Downloads
cd kafka
bin/zookeeper-server-start.sh config/zookeeper.properties

2. To start the server 
cd Downloads
cd kafka
bin/kafka-server-start.sh config/server.properties

3. To check the kafka topic creation and read
   cd Downloads
   cd kafka
   kafka % bin/kafka-topics.sh --create --topic topic-example --bootstrap-server localhost:9092

4. To write to the topic
bin/kafka-console-producer.sh --topic topic-example --bootstrap-server localhost:9092
5. To read from the topic
   bin/kafka-console-consumer.sh --topic topic-example --from-beginning --bootstrap-server localhost:9092 



