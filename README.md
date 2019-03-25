![GitHub](https://img.shields.io/github/license/Thomas-George-T/FlumeHiveTwitterApp.svg)
![GitHub top language](https://img.shields.io/github/languages/top/Thomas-George-T/FlumeHiveTwitterApp.svg)

<p align="center">  
	<br>
		<a href="#">
        	<img height=200 src="https://upload.wikimedia.org/wikipedia/commons/b/bb/Apache_Hive_logo.svg"> 
    	</a>
	<br>
</p>

## Description
We ingest Twitter feed using Flume. The tweets will be stored in the avro schema. To use this data, we create tables using AvroSerde in Hive. Once created this data can be cleansed using tools like OpenRefine,Pig etc. The cleansed data can then be used for visualization.

## Components
* [twitter.conf](twitter.conf) is used to store all the configurations required for ingesting tweets
* [TwitterDataAvroSchema.avsc](Hive%20scripts/TwitterDataAvroSchema.avsc) contains the avro schema.
* [avrodataread.q](Hive%20scripts/avrodataread.q) is used to create a staging table with avro Serde.
* [create_tweets_avro_table.q](Hive%20scripts/create_tweets_avro_table.q) is used to create a processing table with well defined DDL's.

## Prerequisites
To run this software you need the following:
1. Linux 
2. Hadoop 2.0
3. Hive 2.0 
4. Flume
5. Twitter Developer App Credentials

## Steps
1. Get credentials for developing twitter apps.

2. Write a twitter.conf file and replace the variables with your secret keys given by twitter.

3. Execute twitter.conf in the terminal
	```
	flume-ng agent -n TwitterAgent -f $FLUME_CONF_DIR/twitter.conf
	```

4. Get the schema from the avro log file
	```
	hdfs dfs -cat /user/flume/tweets/FlumeData.* | head
	```

5. Copy and then save the schema in a file called `TwitterDataAvroSchema.avsc`

6. Edit the file for readability.

7. Write a hql file called `avrodataread.q` to create table tweets using the AvroSerDe, mention the avro schema file in the tblproperties.

8. Execute the file in terminal
	```
	hive -f FlumeHiveTwitterApp/Hive scripts/avrodataread.q
	```

9. To create a table for processing or for visualization, use the file named `create_tweets_avro_table.q` and execute it.
	```
	hive -f FlumeHiveTwitterApp/Hive scripts/create_tweets_avro_table.q
	```

10. Clean using tools like pig,OpenRefine etc.

11. Visualize the data into a dashboard using tools like tablaeu,d3.js etc.