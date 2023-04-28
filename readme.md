# Docker Compose Setup for Spark and Hadoop with S3 and GCP Storage Support
This Docker Compose setup provides a local development environment for Apache Spark and Apache Hadoop. It also includes support for Amazon S3 and Google Cloud Storage.

## Requirements
* Docker
* Docker Compose
## Usage
 1. Clone this repository.
 2. Run docker-compose up to start the containers.
 3. You can run this on your locally install jupyterlab/pyspark instance requires PySpark Version :3.1.1 !
 4. You may need to edit /etc/hosts on your machine, add 
 
 127.0.0.1       localhost spark-master namenode datanode
 
::1             localhost spark-master namenode datanode

 5. create a spark context on spark://spark-master:7077
## S3 Support
This setup includes the Hadoop S3A filesystem library. To connect to an S3 bucket, you can use the s3a:// prefix in your file paths.

For example, to read a file from an S3 bucket called my-bucket with the file path path/to/my-file.csv, you would use the following code:


spark.read.format('csv').load('s3a://my-bucket/path/to/my-file.csv')
You will need to provide your AWS credentials in the environment variables AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY.

## GCP Storage Support
This setup includes the Hadoop GCS filesystem library. To connect to a GCP Storage bucket, you can use the gs:// prefix in your file paths.

For example, to read a file from a GCP Storage bucket called my-bucket with the file path path/to/my-file.csv, you would use the following code:


spark.read.format('csv').load('gs://my-bucket/path/to/my-file.csv')

You will need to provide your GCP credentials in the environment variable GOOGLE_APPLICATION_CREDENTIALS.

## Volumes
This setup uses volumes to persist Hadoop data between container restarts. The data is stored in the hadoop-data directory. You can change the location of this directory by modifying the volumes section of the namenode and datanode services in the docker-compose.yml file.
## IMPORTANT

if you wish to use your locally installed pyspark, you must mount vulumes to use your own data
I.E  - /Users/nickphom/BigData:/Users/nickphom/BigData in volumes where i have data change to your needs

## Ports
This setup exposes the following ports:

50070: Hadoop NameNode web UI
