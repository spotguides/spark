# Spark with History Server


This spotguide deploys Spark with Spark History Server to a Kubernetes cluster allowing users to submitting and running spark jobs in a namespace on the cluster. 

Spark being deployed is the upstream Spark with a couple of additions from Banzai Cloud such as:
* Spark application execution resiliency implemented with the use of Kubernetes jobs. More details can be found [here](https://banzaicloud.com/blog/spark-resiliency/)
* Checkpointing for Spark streaming application. More details can be found [here](https://banzaicloud.com/blog/spark-checkpointing/)
* Upstream Spark 2.4.3 version on Kubernetes does not support encrypted RPC communication between driver and executors. Support for encrypted RPC communication will be added starting from version 3.0.0 (which is not released yet) thus we backported it into Spark 2.4.3 to make this functionallity available through this Spotguide.
