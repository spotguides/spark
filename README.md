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

  - [Spark 2.4.3 configuration](https://spark.apache.org/docs/2.4.3/running-on-kubernetes.html#configuration)
  - [Spark 2.3.2 configuration](https://spark.apache.org/docs/2.3.2/running-on-kubernetes.html#configuration)

Source files can be placed in source local:/// or s3 / wasbs etc.
Event log can be placed as well on local:/// or s3 / wasbs etc..


In case of Amzanon. google, Alibaba, Oracle clouds the spotguide automatically places the secret keys in a secret, ...
you can only access one bukcet...
In case of Azure you can you different storage accounts ... specifing the access key for each.
