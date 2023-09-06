# Word Count with Hadoop MapReduce and Java

- `WC_Mapper.java`, `WC_Reducer.java`, and `WC_Runner.java` contain the code for Hadoop MapReduce. A JAR file 'word_count_proj-1.0-SNAPSHOT.jar' is created from them.
- `sample.txt` contains sample English text. We'll count the words from this file using the MapReduce program executed on a Hadoop cluster.

## Deploying an Example HDFS Cluster
To deploy an example HDFS cluster, run:
```bash
docker-compose up
```

## Accessing the Master Node (NameNode)
Access the master node 'namenode':
```bash
docker exec -it namenode bash
```

## Creating Folder Structure to Upload Input Files
Create folder structure to upload input files:
```bash
hdfs dfs -mkdir -p /user/root/input
```

We can verify if it was created correctly
```bash
hdfs dfs -ls /user/root
```

## Moving Files into the Container
Move the JAR file & input text file into the container
```bash
docker cp data\word_count_proj-1.0-SNAPSHOT.jar namenode:/tmp
```
```bash
docker cp data\sample.txt namenode:/tmp
```

## Copying the Text File to HDFS Input Directory
Copy the .txt file from /tmp to the hdfs input directory
```bash
hdfs dfs -put tmp/sample.txt /user/root/input
```

## Running the MapReduce Code
Run the MapReduce code on the sample text file and save results in output directory
```bash
hadoop jar word_count_proj-1.0-SNAPSHOT.jar orgwordcount.WC_Runner input/sample.txt output
```

## Viewing Word Count Results
See the word count results
```bash
hdfs dfs -cat /user/root/output/*
```


