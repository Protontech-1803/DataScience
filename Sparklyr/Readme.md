# Processing Data in Spark 3.0 with R programming
In this POC, Data is processed using Spark 3.0 from R program. Using Sparklyr and dplyr packages the DataFrames are processed in Spark 3.0 Environment. 

**The following are the steps to invoke the processing of DataFrames in Spark 3.0 from a R program:**

1.	Install and Configure R, Rstudio and RTools in your local machine.

2.	Install and Configure Spark in your local machine along with Winutils for Hadoop.

3.	Configure the Respective Environment Home Variables and update the PATH.

4.	Launch R Studio and install the sparklyr package along with its dependencies.

5.	Launch the Spark-shell in a Terminal, and verify the connectivity.

     ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/Sparklyr/spark_confirmation.png)
 

6.	Prepare a Sample Data in a CSV file, Further load data from this file using SparkContext.

     ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/Sparklyr/SampleData.png)
 

7.	Run the below steps in R Studio one by one, which is used to connect to Spark, Create SparkContext, Load the CSV and process the CSV in Spark.

        library(sparklyr)
        library(dplyr)
        sc <- spark_connect(master = "local")
        spark_connection_is_open(sc)
        spark_version(sc)
        spark_installed_versions()
        df <- spark_read_csv(sc,"c:/spark/sample.csv")
        head(df)
        filter(df, price<70000)
        select(filter(df,price<70000), street)

   
 8. The output is the processed data as shown below.
 
       ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/Sparklyr/rstudioOutput.png)
 


