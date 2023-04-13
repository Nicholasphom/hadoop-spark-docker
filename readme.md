# Docker Compose Setup for Spark and Hadoop with S3 and GCP Storage Support
This Docker Compose setup provides a local development environment for Apache Spark and Apache Hadoop. It also includes support for Amazon S3 and Google Cloud Storage.

## Requirements
* Docker
* Docker Compose
## Usage
 1. Clone this repository.
 2. Run docker-compose up to start the containers.
 3. Connect to the Jupyter notebook by opening your web browser and navigating to http://localhost:8888. The access token is printed in the console output.
Use the provided pyspark command in the Jupyter notebook to create a SparkSession.
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

## Ports
This setup exposes the following ports:

50070: Hadoop NameNode web UI
8888: Jupyter Notebook
