Instructions to setup the Project:
1. To run the project we need Python 3.6>=, Spark 3.2.1 (PySpark 3.2.1) & Kafka
    Python Installation Guide : https://realpython.com/installing-python/
    Spark Installation Guide : https://spark.apache.org/docs/latest/api/python/getting_started/install.html
    Kafka Installation Guide : https://kafka.apache.org/quickstart, https://www.geeksforgeeks.org/how-to-install-and-run-apache-kafka-on-windows/

    Note : I am using mongodb to ingest all the raw records and for that need to keep two jar file in the jar folder in spark home directory:
            i.  mongo-java-driver-3.12.11.jar 
            ii. mongo-spark-connector-10.0.1.jar
    
    I have kept this jars under lib folder in project.

2. Next step is to create a kafka-topic named "BitCoinTweets" for that first start zookeeper and kafka broker service (https://kafka.apache.org/documentation/#quickstart_startserver).
    Command To create topic:

    i. linux/macOs : bin/kafka-topics.sh --create --topic BitCoinTweets --bootstrap-server localhost:9092
    ii. windows : .\bin\windows\kafka-topics.bat --create --topic BitCoinTweets -- --bootstrap-server localhost:9092

To verify we can list topics in kafka by command: bin/kafka-topics.sh --describe --topic BitCoinTweets --bootstrap-server localhost:9092

4. I have kept dataset CSV files in a zip on Amazon S3 to download it following is the link:
    

3. Third step is to run Setup.py to install all dependencies (change terminal or command-prompt directory to the project) and with this step project set-up is completed. 
    command : python .\Setup.py

4. Now, First we will run spark-streaming job using spark-submit, with following command.
    command : spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.1.2,org.apache.kafka:kafka-clients:2.8.1 .\Kafka_Streaming\BitCoinTweetDataIngestionStreaming.py > .\Kafka_Streaming\logs\application.log

5. After starting streaming spark job we will start KafkaProducer.py to push records in topic "BitCoinTweets".
    command: python .\Kafka_Streaming\KafkaProducer.py

6. As ingestion finishes we can move to Analysis phase and open ".\Analysis\BitcoinTweetsAnalysis.ipynb" in  jupyter.

Notes :
1. Please stop services : zookeeper & kafka-broker
2. Please spark streaming spark job after ingestion.
