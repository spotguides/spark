# Spark with History Server


This spotguide deploys Spark with Spark History Server to a Kubernetes cluster allowing users to submitting and running spark applications in a namespace on the cluster.

Spark being deployed is the upstream Spark with a couple of additions from Banzai Cloud such as:
* Spark application execution resiliency implemented with the use of Kubernetes jobs. More details can be found [here](https://banzaicloud.com/blog/spark-resiliency/)
* Checkpointing for Spark streaming application. More details can be found [here](https://banzaicloud.com/blog/spark-checkpointing/)
* Upstream Spark 2.4.3 version on Kubernetes does not support encrypted RPC communication between driver and executors. Support for encrypted RPC communication will be added starting from version 3.0.0 (which is not released yet) thus we backported it into Spark 2.4.3 to make this functionality available through this Spotguide.

You can choose between version the following Spark versions: 2.4.3, 2.3.2.
In version 2.3.2 you can run only applications written in Scala, while in case of 2.4.3 you can run Python and R code as well. The following encryption options are also available in 2.4.3 :

```
spark.authenticate=true
spark.network.crypto.enabled=true
spark.io.encryption.enabled=true
```

Once your spotguide is deployed successfully, you should have an up and running History Server plus RBAC resources needed to be able to submit Spark applications with spark-submit.
You can find a good description of Kubernetes related spark-submit options below:

  - [Spark 2.4.3 configuration options](https://spark.apache.org/docs/2.4.3/running-on-kubernetes.html#configuration)
  - [Spark 2.3.2 configuration options](https://spark.apache.org/docs/2.3.2/running-on-kubernetes.html#configuration)

Spark on Kubernetes currently is not able to access he submission client’s local file system, you must either
build your source files, dependencies into Spark Docker image, or if they must be hosted in remote locations like HDFS or HTTP.
Object storages like S3, Azure Blob, Google Storage, Oracle Blob Storage, OSS are supported through corresponding HDSF connectors.
Spark File API is also able to access these storages, event logs can be placed here as well, just be aware that apart from Azure Storage you can not use different storage credentials for an Object Storage, like you can not specify different AWS credentials for your source files and Spark event log files in S3.

Checkout the below table which prefix to use in case of different storages:

| Storage   | Prefix | Example                                                       |Credentials                           |
| ------------------------------------ | ---------|----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| local in Docker image                     | local      | local:///opt/spark/examples/src/main/python/pi.py | - |
| Amazon S3 | s3, s3a      | s3a://bucketName/sample.txt | AWS credentials must be set in the following configuration properties for spark-submit: *spark.hadoop.fs.s3a.access.key* and *spark.hadoop.fs.s3a.secret.key* |
| Azure Blob | wasb, wasbs      | wasb://exampleAzureBlobName@exampleStorageAccountName.blob.core.windows.net | Azure storage account access key must be set as follows: *spark.hadoop.fs.azure.account.key.exampleStorageAccountName.blob.core.windows.net=storageAccountAccessKey* |
| Google Cloud Storage | gs      | gs://bucketName | - |
| Alibaba Object Storage | oss      | oss://bucketName | - |
| Oracle Cloud Storage | oci      | oci://bucketName | - |
