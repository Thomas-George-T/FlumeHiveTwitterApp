# Aim
Ingesting tweets using Flume and then creating hive tables for further processing.

# Description
Twitter feed ingested using Flume is in avro format. To use this data you have to use the AvroSerde in hive to create tables. Once created this data can be used cleaned using Tools like Pig.

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
4. get the schema from the avro log file
```
hdfs dfs -cat /user/flume/tweets/FlumeData.* | head
```
5. Copy and then save the schema in a file called `TwitterDataAvroSchema.avsc`
6. Edit the file for readability.
7. Write a hql file called `avrodataread.hql` to create table tweets using the AvroSerDe, mention the avro schema file in the tblproperties.
8. Execute the file in terminal
```
hive -f FlumeHiveTwitterApp/Hive scripts/avrodataread.hql
```
9. To create a table for processing using pig or for visualization, use the file named `create_tweets_avro_table.hql` and execute it.
```
hive -f FlumeHiveTwitterApp/Hive scripts/create_tweets_avro_table.hql
```
10. Clean using pig.

## To Do (Remaining for completion)
- [x] Get Twitter App Credentials 
- [x] Set up twitter.config 
- [x] Write hql using AvroSerde to store tweets. 
- [ ] Process and clean the data using Pig
- [ ] Include references and related links 

