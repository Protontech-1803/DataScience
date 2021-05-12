# Backup and Restore the files and directories of HDFS file system using Hadoop

This POC illustrates how to take a backup and restore the files and directories in HDFS file system by using Hadoop commands.

**The following are the steps to back up and restore the files and directories:**

1.	Create Hadoop Cluster and run HDFS service in the cluster.

    ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/HDFS_Snapshot/Img1.jpg)

2.	Create a directory in HDFS file system using Hadoop command.

    ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/HDFS_Snapshot/Img2.jpg)

3.	Create a file **sample.txt** in **/user/cloudera/example** directory.

    ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/HDFS_Snapshot/Img3.jpg)

4.	Create the backup of the directory **/user/cloudera/example** in Hadoop File system using Hadoop commands.
    
      a.	Allow Hadoop to create the snapshot(backup) in Hadoop File system.
                    
      ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/HDFS_Snapshot/Img4.jpg)

      b.	Create a snapshot of the directory by executing Hadoop createSnapshot command.
      
      ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/HDFS_Snapshot/Img5.jpg)

      c.	Rename the snapshot by executing Hadoop renameSnapshot command.
      
      ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/HDFS_Snapshot/Img6.jpg)

      d.	List the directory to view the snapshot created in the directory.
      
      ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/HDFS_Snapshot/Img7.jpg)

5.	Restore the snapshot created in the previous step. 

    a.	Copy the **snapshot1** from HDFS file system and paste it in your local file system.
    
    ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/HDFS_Snapshot/Img8.jpg)

    b.	Verify the restored file **snapshot1** in local file system.

     ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/HDFS_Snapshot/Img9.jpg)








