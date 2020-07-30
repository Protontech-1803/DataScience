# Spark Streaming with Movie Dataset


In this POC, a movie rating data set is analyzed using Spark. As a result of analysis, the count of star ratings that are given by various users for a given movie is displayed.

**Below are the steps to load and filter the dataset with respect to a movie rating:**  
          **_Note:_**  *The Movie is Rated between the range [1-5] stars in the dataset.*
   
  1. Consider a Movie Rating Data Set in the file. For example, ml-100k.zip.

  2. Extract the file and move the file to the respective folder.

  3. Launch Eclipse IDE and create a new Spark Scala Project. Add the below code in the IDE, where the **countby** operation gives the count of star rating given by the users for a given movie data set.
  
  
          package com.movies.spark

          import org.apache.spark._
          import org.apache.spark.SparkContext._
          import org.apache.log4j._

          /** Count up how many of each star rating exists in the MovieLens 100K data set. */
          object RatingsCounter {

            /** Our main function where the action happens */
            def main(args: Array[String]) {

              // Set the log level to only print errors
              Logger.getLogger("org").setLevel(Level.ERROR)

              // Create a SparkContext using every core of the local machine, named RatingsCounter
              val sc = new SparkContext("local[*]", "RatingsCounter")

              //Load the data
              // Load up each line of the ratings data into an RDD
              val lines = sc.textFile("../ml-100k/u.data")

              //Extracting the files
              // Convert each line to a string, split it out by tabs, and extract the third field.
              // (The file format is userID, movieID, rating, timestamp)
              val ratings = lines.map(x => x.toString().split("\t")(2))

              //Perform countByValue based on rating of the movie
              // Count up how many times each value (rating) occurs
              val results = ratings.countByValue()

              //sort the data
              // Sort the resulting map of (rating, count) tuples
              val sortedResults = results.toSeq.sortBy(_._1)

              //display the data
              // Print each result on its own line.
              sortedResults.foreach(println)
            }
          }

  
  
      ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/SparkStreaming/RatingsCounter.png)
   
  4.	The output shows the Star ratings number, given by various users for the movie.
     ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/SparkStreaming/OutPut.png)
