# Import and Process JSON Data using R Programming

#### In this POC, JSON Data Source is imported and the imported data is processed using R Programming features. 

#### The following are the steps to Import and Process the data using R Programming.

1.	In RStudio IDE, Install the rjson Package along with its dependencies by downloading it from CRAN Respository. Also verify that libraries for rjson is installed from the RConsole.

![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/Process%20Data%20using%20R/png/1.png)
 
2.	Using RStudio IDE create a R Script, with the below code. The Code Loads the rjson package, which is used to load the data in the JSON file into the DataFrame. 

![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/Process%20Data%20using%20R/png/2.png)
 
3.	On Running this code in the RConsole the sample "family.json" file is read from the current working directory. The Data is read from the JSON file and stored in the DataFrame. Further this DataFrame can be processed using R Programming Features.
4.	To Display the DataFrame Contents, print command is used in the code. On Execution of Print Command the contents of the DataFrame is displayed as shown below.  
 
![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/Process%20Data%20using%20R/png/3.png)
