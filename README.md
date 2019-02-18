# Sqoop
Using sqoop to copy data from SQLServer to Hadoop


## Sqoop Introduction
Apache Sqoop is a tool designed for efficiently transferring bulk data to and from structured datastores (SQL Server, MySQL) and Apache Hadoop.
You can use Sqoop to import data from external structured datastores into Hadoop Distributed File System or related systems like Hive and HBase.
It efficiently transfers bulk data between Hadoop and external data stores such as enterprise data warehouses, relational databases, etc.
Conversely, Sqoop can be used to extract data from Hadoop and export it to external structured datastores such as relational databases and enterprise data warehouses.

 
This is how Sqoop got its name – “SQL to Hadoop & Hadoop to SQL”


## Key Features of Sqoop

Sqoop provides many salient features like:

Full Load: Apache Sqoop can load the whole table by a single command. You can also load all the tables from a database using a single command.
Incremental Load: Apache Sqoop also provides the facility of incremental load where you can load parts of table whenever it is updated.
Parallel import/export: Sqoop uses YARN framework to import and export the data, which provides fault tolerance on top of parallelism.
Import results of SQL query: You can also import the result returned from an SQL query in HDFS.
Compression: You can compress your data by using deflate(gzip) algorithm with –compress argument, or by specifying –compression-codec argument. You can also load compressed table in Apache Hive.
Connectors for all major RDBMS Databases: Apache Sqoop provides connectors for multiple RDBMS databases, covering almost the entire circumference.
Kerberos Security Integration: Kerberos is a computer network authentication protocol which works on the basis of ‘tickets’ to allow nodes communicating over a non-secure network to prove their identity to one another in a secure manner. Sqoop supports Kerberos authentication.
Load data directly into HIVE/HBase: You can load data directly into Apache Hive for analysis and also dump your data in HBase, which is a NoSQL database.
Support for Accumulo: You can also instruct Sqoop to import the table in Accumulo rather than a directory in HDFS


## Basic Available commands
 

  codegen           	Generate code to interact with database records
  create-hive-table 	Import a table definition into Hive
  eval              	Evaluate a SQL statement and display the results
  export            	Export an HDFS directory to a database table
  help              	List available commands
  import            	Import a table from a database to HDFS
  import-all-tables 	Import tables from a database to HDFS
  import-mainframe  	Import datasets from a mainframe server to HDFS
  job               	Work with saved jobs
  list-databases    	List available databases on a server
  list-tables       	List available tables in a database
  merge             	Merge results of incremental imports
  metastore         	Run a standalone Sqoop metastore
  version           	Display version information
