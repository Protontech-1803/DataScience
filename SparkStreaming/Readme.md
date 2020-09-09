# Streaming Data from Kafka Topic using Spark 3.0

In this POC Streaming job (Spark Application) will run for every 10 seconds and it will do the wordcount on the data it has received in those 10 seconds from the Kafka Topic. By sending a message from the producer console, the Spark Application will do the word count instantly and return the results. 

**The Following are the Implementation Steps.**

1.	Install and Configure Apache Zookeeper 3.6.1 on windows OS-based Machine.

2.	Install and Configure Apache Kafka on windows OS-based Machine.

3.	Configure the dataDir parameter in zoo.cfg Apache Zookeeper Configuration file.

4.	Set the log.dirs property in Kafka server properties in the folder kafka/config.

5.	Run zkserver command to start the apache zookeeper, followed by this start Apache Kafka by running the below command.


        .\bin\windows\kafka-server-start.bat .\config\server.properties
       
  
      ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/SparkStreaming/SparkStreamingPNG/Start_Zookeeper.png) 
      
  
  
6.	Create a Topic called wordcountspark in Apache Kafka by running the below command.


        kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic wordcountspark
              

      ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/SparkStreaming/SparkStreamingPNG/WordCountSpark.png)
      
 

7.	Use a producer console for sending messages continuously to the topic workcountspark using the below command.


        kafka-console-producer.bat --broker-list localhost:9092 --topic wordcountspark
       

      ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/SparkStreaming/SparkStreamingPNG/Message_WordCountSpark.png)
      

 
8.	Create a Work Count Scala Program with Spark Streaming the Kafka topic using the below code in Eclipse IDE.


            package com.test
            import org.apache.spark.SparkConf
            import org.apache.spark.streaming.StreamingContext
            import org.apache.spark.streaming.Seconds
            import org.apache.spark.streaming.kafka.KafkaUtils
            object WordCount {
              def main( args:Array[String] ){
                val conf = new SparkConf().setMaster("local[*]").setAppName("KafkaReceiver")
                val ssc = new StreamingContext(conf, Seconds(10)
                val kafkaStream = KafkaUtils.createStream(ssc, "localhost:2181","spark-streaming-consumer-group", Map("wordcountspark" -> 5))
                //need to change the topic name and the port number accordingly
                val words = kafkaStream.flatMap(x =>  x._2.split(" "))
                val wordCounts = words.map(x => (x, 1)).reduceByKey(_ + _)
                kafkaStream.print()  //prints the stream of data received
                wordCounts.print()   //prints the wordcount result of the stream
                ssc.start()
                ssc.awaitTermination()
               }
            }


      ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/SparkStreaming/SparkStreamingPNG/WordCountSpark_Program.png)


9.	Run the Spark Application in the IDE, and enter some lines of text in the producer command prompt. you will see the output of the application execution, with the wordcount output of the input text in the producer command prompt.


      ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/SparkStreaming/SparkStreamingPNG/output.png)
 
 
 

