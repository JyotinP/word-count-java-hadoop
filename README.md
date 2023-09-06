# word-count-java-hadoop
Counting words with Hadoop MapReduce and Java

-- WC_Mapper.java, WC_Reducer.java & WC_Runner.java has the code for Hadoop MapReduce. JAR file 'word_count_proj-1.0-SNAPSHOT.jar' is created from them.
-- sample.txt contains sample english text. We'll count the words from this file using the MapReduce program executed on a Hadoop cluster.

-- To deploy an example HDFS cluster, run:
docker-compose up

-- Access the master node 'namenode':
docker exec -it namenode bash

-- Create folder structure to upload input files:
hdfs dfs -mkdir -p /user/root/input

-- We can verify if it was created correctly
hdfs dfs -ls /user/root

-- Move the JAR file & input text file into the container
docker cp data\word_count_proj-1.0-SNAPSHOT.jar namenode:/tmp
docker cp data\sample.txt namenode:/tmp

-- Copy the .txt file from /tmp to the hdfs input directory
hdfs dfs -put tmp/sample.txt /user/root/input

-- Run the MapReduce code on the sample text file and save results in output directory
hadoop jar word_count_proj-1.0-SNAPSHOT.jar orgwordcount.WC_Runner input/sample.txt output

-- See the word count results
hdfs dfs -cat /user/root/output/*
