# Scheduling Oozie Workflow on Cloudera


Scheduling the Oozie Workflow to execute the Sqoop import job from SQL RDBMS to HDFS at the given frequency. Coordinator file consists of the task start and end time with the frequency scheduled. On successful execution it is verified in the HUE UI.


**Steps to Schedule Oozie Workflow on Cloudera are:**

1.	Create Sqoop workflow file using vi editor in HDFS (cloudera) as shown below.

    ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/Scheduling%20Oozie%20Workflow/Scheduling%20Oozie%20Workflow%20PNG/sqoopworkflow.png)
   
 
2.	Copy the below code and paste it in the Vi Editor and save the file.

       <workflow-app name="Sqoop_Import" xmlns="uri:oozie:workflow:0.4">
       <global>
       <job-tracker>${jobTracker}</job-tracker>
       <name-node>${nameNode}</name-node>
       </global>
       <start to="full_table" />
       <!-- Unload the data from Source Schema and stores in Hdfs path for full refresh modes -->
       <action name="full_table" >
       <sqoop xmlns="uri:oozie:sqoop-action:0.2">
       <job-tracker>${jobTracker}</job-tracker>
       <name-node>${nameNode}</name-node>
       <arg>import</arg>
       <arg>--connect</arg>
       <arg>jdbc:mysql://quickstart.cloudera:3306/retail_db</arg>
       <arg>--target-dir</arg>
       <arg>/user/root/oozie_wflow</arg>
       <arg>--m</arg>
       <arg>1</arg>
       <arg>--mapreduce-job-name</arg>
       <arg>sqoopoozie</arg>
       <arg>--username</arg>
       <arg>retail_dba</arg>
       <arg>--password</arg>
       <arg>cloudera</arg>
       <arg>--table</arg>
       <arg>categories</arg>
       <arg>--null-string</arg>
       <arg>""</arg>
       <arg>--null-non-string</arg>
       <arg>""</arg>
       <arg>--verbose</arg>
       </sqoop>
       <ok to="end" />
       <error to="end" />
       </action>
       <end name="end"/>
       </workflow-app>


3.	Create job.properties file using vi editor in HDFS (cloudera) as shown below.
   
    ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/Scheduling%20Oozie%20Workflow/Scheduling%20Oozie%20Workflow%20PNG/job-properties.png)
   
 
4.	Copy the below code and paste it in the Vi Editor and save the file.

       nameNode=hdfs://quickstart.cloudera:8020
       jobTracker=quickstart.cloudera:8032
       queueName=default
       oozie.use.system.libpath=true
       oozie.wf.subworkflow.classpath.inheritance=true
       oozie.action.sharelib.for.pig=pig,hcatalog
       oozie_action_sharelib_for_hive=hive2
       oozie_launcher_action_main_class=org.apache.oozie.action.hadoop.Hive2Main
       sqoop_jar=/user/oozie/share/lib/sqoop/sqoop-1.4.6-cdh5.7.0.jar
       mysql_jar=/mysql-connector-java-5.1.48/mysql-connector-java-5.1.48.jar
       #workflow
       oozie.coord.application.path=/user/root/sqoop_import/coordinator.xml
       #oozie.wf.application.path=/user/cloudera/workflows/sqoopworkflow.xml
       oozie.libpath=/user/oozie/share/lib/sqoop


5.	Create Coordinator file using vi editor in HDFS (cloudera) as shown below.
   
    ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/Scheduling%20Oozie%20Workflow/Scheduling%20Oozie%20Workflow%20PNG/coordinator-file.png)
    
 
6.	Copy the below code and paste it in the Vi Editor and save the file.

        <coordinator-app timezone="UTC" end="2021-02-17T12:48Z" start="2021-02-17T11:48Z" frequency="5 " name="sqoop-import" xmlns="uri:oozie:coordinator:0.2">
       <controls>
       <execution>FIFO</execution>
       </controls>
       <action>
       <workflow>
       <app-path>/user/root/workflows/sqoopworkflow.xml</app-path>
       </workflow>
       </action>
       </coordinator-app>


7.	Execute the below shown command to run the Oozie workflow for Sqoop.
   
    ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/Scheduling%20Oozie%20Workflow/Scheduling%20Oozie%20Workflow%20PNG/submitWorkflow.png)
   
 
8.	On successful submission of the job to run, a workflow job ID will be displayed as shown below. 
   
    ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/Scheduling%20Oozie%20Workflow/Scheduling%20Oozie%20Workflow%20PNG/JobID.png)
   
 
9.	Execute the below shown command with the Workflow ID in the terminal to view the status of the respective job.

    ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/Scheduling%20Oozie%20Workflow/Scheduling%20Oozie%20Workflow%20PNG/Job-Info.png)
   
 
10. Open HUE UI, Ooozie dashboard to verify the status of the Workflow.
    
     ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/Scheduling%20Oozie%20Workflow/Scheduling%20Oozie%20Workflow%20PNG/HUE%20UI-OozieDashboard.png)
    
 
11. In HUE UI, Ooozie dashboard to verify the status of Jobs in Coordinators panel.
   
     ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/Scheduling%20Oozie%20Workflow/Scheduling%20Oozie%20Workflow%20PNG/HUE-CoordinatorsPanel.png)
   
 
12.	On successful execution verify the file imported according to the workflow.
    
     ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/Scheduling%20Oozie%20Workflow/Scheduling%20Oozie%20Workflow%20PNG/HUE-fileImported.png)
    
 
13.	Open the HUE UI File Browser and check the target directory existence as shown below.
Target directory: /user/root /oozie_wflow.

   ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/Scheduling%20Oozie%20Workflow/Scheduling%20Oozie%20Workflow%20PNG/HUE-targetDirectory.png)
 
14.	On successful execution, verify the content of the file is successfully imported to HDFS.
    
     ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/Scheduling%20Oozie%20Workflow/Scheduling%20Oozie%20Workflow%20PNG/HUE-content-in-HDFS.png)
     
 


