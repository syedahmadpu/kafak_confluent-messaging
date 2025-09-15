# Real-Time Data Pipeline with Python and Confluent Kafka 🚀

This project demonstrates a foundational, end-to-end real-time data pipeline built using Python and Confluent Kafka. It simulates a common data engineering scenario where data is ingested from a static source (a CSV file), published to a distributed message bus, and then processed in real-time by a downstream consumer.

The project is divided into two main components:
* `Confluent-KafkaProduce.ipynb`: The Kafka producer that reads data and sends it to a topic.
* `Consume_Message.ipynb`: The Kafka consumer that subscribes to the topic and processes incoming messages.

## Project Workflow

1.  **Data Ingestion**: A producer script reads customer data from a local CSV file using the pandas library.
2.  **Data Serialization**: Each row from the CSV is converted into a structured JSON format.
3.  **Message Production**: The producer connects to a Confluent Cloud Kafka cluster and sends each JSON record as a message to the `ecommerce` topic. The `customer_id` is used as the message **key** to ensure data for the same customer is sent to the same partition, preserving order.
4.  **Message Consumption**: A separate consumer script connects to the same Confluent Cloud cluster, subscribes to the `ecommerce` topic as part of a consumer group, and begins listening for messages from the earliest offset.
5.  **Data Processing**: As messages are received, the consumer decodes the key and JSON value and prints the customer data to the console, demonstrating a successful end-to-end data flow.

## Key Concepts Demonstrated
* **Kafka Producer/Consumer Development**: Custom Python scripts built using the `confluent-kafka` library to produce and consume messages.
* **Topic Architecture**: Creation and utilization of a Kafka topic (`ecommerce`) for a specific data stream.
* **Data Serialization**: Converting raw data (CSV) into a structured message format (JSON) suitable for streaming applications.
* **Message Keys**: Using a business key (`customer_id`) to control data partitioning and guarantee in-order processing for related events.
* **Consumer Groups**: Implementing a consumer as part of a consumer group (`customer_group`), which is the foundation for scalable and parallel data processing in Kafka.

## Technology Stack
* **Platform**: Confluent Cloud
* **Core Technology**: Apache Kafka
* **Language & Libraries**: Python, `confluent-kafka`, `pandas`
* **Data Formats**: JSON, CSV
* **Kafka APIs**: Producer API, Consumer API
