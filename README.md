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
  
  
  
  Sqoop – IMPORT Command
Import command is used to importing a table from relational databases to HDFS. In our case, we are going to import tables from MySQL databases to HDFS. 
As you can see in the below image, we have employees table in the employees database which we will be importing into HDFS.

sqoop import --connect jdbc:mysql://localhost/employees --username ADP --table employees


Sqoop – IMPORT Command with target directory
You can also import the table in a specific directory in HDFS using the below command

sqoop import --connect jdbc:mysql://localhost/employees --username ADP --table employees --m 1 --target-dir /employees
Sqoop imports data in parallel from most database sources. -m property is used to specify the number of mappers to be executed. 
Sqoop imports data in parallel from most database sources. You can specify the number of map tasks (parallel processes) to use to perform the import by using the -m or –num-mappers argument. Each of these arguments takes an integer value which corresponds to the degree of parallelism to employ. 

You can control the number of mappers independently from the number of files present in the directory. Export performance depends on the degree of parallelism. By default, Sqoop will use four tasks in parallel for the export process. This may not be optimal, you will need to experiment with your own particular setup. Additional tasks may offer better concurrency, but if the database is already bottlenecked on updating indices, invoking triggers, and so on, then additional load may decrease performance.

 

Sqoop – IMPORT Command with Where Clause

You can import a subset of a table using the ‘where’ clause in Sqoop import tool. It executes the corresponding SQL query in the respective database server and stores the result in a target directory in HDFS. You can use the following command to import data with ‘where‘ clause: 
sqoop import --connect jdbc:mysql://localhost/employees --username ADP --table employees --m 3 --where "emp_no &gt; 700" --target-dir /Latest_Employees
 

 

 

Sqoop – Incremental Import

sqoop import --connect jdbc:mysql://localhost/employees --username ADP --table employees --target-dir /Latest_Employees --incremental append --check-column emp_no --last-value 700

Sqoop provides an incremental import mode which can be used to retrieve only rows newer than some previously-imported set of rows. Sqoop supports two types of incremental imports: append and lastmodified. You can use the –incremental argument to specify the type of incremental import to perform.
You should specify append mode when importing a table where new rows are continually being added with increasing row id values. You specify the column containing the row’s id with –check-column. Sqoop imports rows where the check column has a value greater than the one specified with –last-value.
An alternate table update strategy supported by Sqoop is called lastmodified mode. You should use this when rows of the source table may be updated, and each such update will set the value of a last-modified column to the current timestamp.

When running a subsequent import, you should specify –last-value in this way to ensure you import only the new or updated data. This is handled automatically by creating an incremental import as a saved job, which is the preferred mechanism for performing a recurring incremental import.

 

 

Sqoop – Import All Tables
You can import all the tables from the RDBMS database server to the HDFS. Each table data is stored in a separate directory and the directory name is same as the table name. It is mandatory that every table in that database must have a primary key field. The command for importing all the table from a database is:

 

sqoop import-all-tables --connect jdbc:mysql://localhost/employees --username ADP
 

Sqoop – List Tables
You can also list out the tables of a particular database in MySQL database server using Sqoop. Sqoop list-tables tool parses and executes the ‘SHOW TABLES’ query. The command for listing tables is a database is:

 

sqoop list-tables --connect jdbc:mysql://localhost/employees --username ADP
 


 
Sqoop – Export
The command to export data from HDFS to the relational database is:

 

sqoop export --connect jdbc:mysql://localhost/employees --username ADP --table emp --export-dir /user/edureka/employees
 

 

 

Sqoop – Codegen
In object-oriented application, every database table has one Data Access Object class that contains ‘getter’ and ‘setter’ methods to initialize objects. Codegen generates the DAO class automatically. It generates DAO class in Java, based on the Table Schema structure.
The command for generating java code is:

sqoop codegen --connect jdbc:mysql://localhost/employees --username ADP  --table employees






Sqoop – Import a specific table from SQL Server to HIVE
--table is a relational database table to read the source.
-m 1 is representing the mappers, by specifying -m 1 means you need only one mapper to be run to import the table. This is used for controlling parallelism. To achieve the parallelism Sqoop uses the primary key/unique key to split the rows from source table.
--input-fields-terminated-by is the option used during Sqoop Export (i.e. they are Input Formatting arguments) which describe how the input data is present in HDFS before exporting to RDBMS.
--hive-import, Sqoop will first do a normal HDFS import to a temporary location. After a successful import, Sqoop generates two queries: one for creating a table and another one for loading the data from a temporary location. You can specify any temporary location using either the --target-dir or --warehouse-dir parameter.
--hive-table <table-name> sets the table name to use when importing to Hive.

sqoop import --connect
"jdbc:sqlserver://ROSQC50;databaseName=ETLDB;" \
--username IEHUBETLLogin --password IEHUBETLLogin \
--table "EE_ParticipantAccount" -m 1 \
--fields-terminated-by "," \
--hive-import \
--hive-table rs.EE_ParticipantAccount_test2



