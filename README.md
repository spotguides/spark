# Spark with History Server


This spotguide deploys Spark with Spark History Server to a Kubernetes cluster allowing users to submitting and running spark applications in a namespace on the cluster.

Spark being deployed is the upstream Spark with a couple of additions from Banzai Cloud such as:
* Spark application execution resiliency implemented with the use of Kubernetes jobs. More details can be found [here](https://banzaicloud.com/blog/spark-resiliency/)
* Checkpointing for Spark streaming application. More details can be found [here](https://banzaicloud.com/blog/spark-checkpointing/)
* Upstream Spark 2.4.3 version on Kubernetes does not support encrypted RPC communication between driver and executors. Support for encrypted RPC communication will be added starting from version 3.0.0 (which is not released yet) thus we backported it into Spark 2.4.3 to make this functionality available through this Spotguide.

Once your spotguide is deployed successfully, you should have an up and running History Server plus RBAC resources needed to be able to submit Spark applications with spark-submit.
You can find a good description on spark-submit options here: https://spark.apache.org/docs/2.4.3/running-on-kubernetes.html#configuration.
