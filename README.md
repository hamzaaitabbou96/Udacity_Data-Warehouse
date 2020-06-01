# Introduction
A music streaming service, called Sparkify, has become more popular. This not only grew their user base, but also their song database. Because of this growth, they would like to move their processes and data onto the cloud. The data for both song details and user activity are currently stored in JSON files.

As more and more data is collected, the more difficult it will be for Sparkify to process and analyses the data in the current JSON format. This is where Amazon Web Server (AWS) and Redshift come in to save the day.

# Project Details
For this project, I will be moving two data sources from a public S3 buckets to Amazon Web Services.

## S3 Buckets (Data Storage):
Bucket 1 contains info about songs and artists
- SONG_DATA='s3://udacity-dend/song_data'
Bucket 2 contains has info about actions done by users (such as what song are listening, etc..)
- LOG_DATA='s3://udacity-dend/log_data'
**Note** we will need a descriptor file (also a JSON) in order to extract the data from the folders. A descriptor file is needed since we do not have a common prefix in the folders.

## Amazon Web Services:
We will be taking the data from the S3 buckets and loading into Redshift, which is a Data Warehouse with columnar storage. Moving the data to this cloud service will help retrieve data faster and store large amounts of it.

To improve our data structure, we will be using a STAR schema. This schema consists of one fact table referencing any number of dimension tables, which helps the Sparkify for solving simplified common business logic.

- **Fact Table:** songplays: attributes referencing to the dimension tables
- **Dimension Tables:** users, songs, artists and time table



# How to run process
1. Start up a AWS Redshift Cluster
- Make sure to setup the IAM role to AmazonS3ReadOnlyAccess.
- Use dc2.large cluster with 4 nodes. Note that each node a cost of USD 0.25/h (on-demand option) per cluster

2. Open up a terminal session or open run_script.ipynb

3. Run '%run create_tables.py'
- This will create the tables, must be run first

4. Run 'python etl.py'
- This will run the ETL process


# ETL.py

### ETL Process
For this project, we use SQL for the ETL and python as a bridge. The transformation and data normalization is done by Query, see the sql_queries.py for more details.
etl.py is where you'll load data from S3 into staging tables on Redshift and then process that data into your analytics tables on Redshift.

ETLPipeline:

1- Implement the logic in etl.py to load data from S3 to staging tables on Redshift.
2- Implement the logic in etl.py to load data from staging tables to analytics tables on Redshift.
3- Test by running etl.py after running create_tables.py and running the analytic queries on your Redshift database to compare your results with the expected results.
4- Delete your redshift cluster when finished.


 # Project Structure
- create_tables.py - Script will drop old tables (if exist) ad re-create new tables
- etl.py - Script will executes the queries that extract JSON data from the S3 bucket and ingest them to Redshift
- sql_queries.py - File that contains variables with SQL statement in String formats, partitioned by CREATE, DROP, COPY and INSERT statements
- dhw.cfg - Configuration file used that contains info about Redshift, IAM and S3


 
 


