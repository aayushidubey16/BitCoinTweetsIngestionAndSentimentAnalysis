Instructions to setup the Project:
1. To run the project we need Python 3.6>=, Spark 3.2.1 (PySpark 3.2.1) & Kafka <br/>
    Python Installation Guide : https://realpython.com/installing-python/ <br/>
    Spark Installation Guide : https://spark.apache.org/docs/latest/api/python/getting_started/install.html <br/>
    Kafka Installation Guide : https://kafka.apache.org/quickstart, https://www.geeksforgeeks.org/how-to-install-and-run-apache-kafka-on-windows/ <br/>
 <br/>
    Note : I am using mongodb to ingest all the raw records and for that need to keep two jar file in the jar folder in spark home directory: <br/>
            i.  mongo-java-driver-3.12.11.jar <br/>
            ii. mongo-spark-connector-10.0.1.jar <br/>
     <br/>
    I have kept this jars under lib folder in project. <br/>
 <br/>
2. Next step is to create a kafka-topic named "BitCoinTweets" for that first start zookeeper and kafka broker service (https://kafka.apache.org/documentation/#quickstart_startserver). <br/>
    Command To create topic: <br/>
 <br/>
    i. linux/macOs : bin/kafka-topics.sh --create --topic BitCoinTweets --bootstrap-server localhost:9092 <br/>
    ii. windows : .\bin\windows\kafka-topics.bat --create --topic BitCoinTweets -- --bootstrap-server localhost:9092 <br/>
 <br/>
To verify we can list topics in kafka by command: bin/kafka-topics.sh --describe --topic BitCoinTweets --bootstrap-server localhost:9092 <br/>
 <br/>
4. I have kept dataset CSV files in a zip on Amazon S3 to download it following is the link: <br/>
     <br/>
3. Third step is to run Setup.py to install all dependencies (change terminal or command-prompt directory to the project) and with this step project set-up is completed.  <br/>
    command : python .\Setup.py <br/>
 <br/>
4. Now, First we will run spark-streaming job using spark-submit, with following command. <br/>
    command : spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.1.2,org.apache.kafka:kafka-clients:2.8.1 .\Kafka_Streaming\BitCoinTweetDataIngestionStreaming.py > .\Kafka_Streaming\logs\application.log  <br/>
 <br/>
5. After starting streaming spark job we will start KafkaProducer.py to push records in topic "BitCoinTweets". <br/>
    command: python .\Kafka_Streaming\KafkaProducer.py  <br/>
 <br/>
6. As ingestion finishes we can move to Analysis phase and open ".\Analysis\BitcoinTweetsAnalysis.ipynb" in  jupyter. <br/>
 <br/>
Notes : <br/>
1. Please stop services : zookeeper & kafka-broker <br/>
2. Please spark streaming spark job after ingestion. <br/>
 <br/>
