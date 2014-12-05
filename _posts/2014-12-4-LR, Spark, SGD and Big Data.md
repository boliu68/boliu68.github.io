---
layout: post
categories: [Algorithm, Machine Learning]
---

#LR, Spark, SGD and Big Data
---

Logistic Regression([LR][1]) serves as a simple but competitive algorithm for classifiation. LR is effective to train and widely utilized online for recommendation, ads and rankings. In this blog, I will demonstrate my experience of LR algorithm based on Stochastic Gradient Descent([SGD][2]), [Spark][3] for quite big dataset. The method is based on python. Some python packages such as numpy, scipy as well as sklearn is utlized for efficiency. It will not be difficult to transfer to other platform, in my opinion.


The so called big data, in this post, represents billions instance(10e9) and billions dimensions(10e8). No doubt that the dimension is very very sparse. On average, only 64 non-zero entries exist for each instance. Concerned about many issuse ^-^. I only talks about pseudo-cdoe as follows.

	Spark_LR(dataset)
	#dataset: #instnaces * #dimension
	#parameters: #partitions,#parallelism
	1 Read data and split each line, repartition the dataset
	2 Build the hash map for features
	3 Dummy(intersection) the features and record the non-zero coordinate/value
	4
	5 #building csr_matrix in scipy is expensive in both memory and computation.
	6 data_rdd = spark.MapPartitions(convert to scipy.csr_matrix).cache()
	7 count the #instance, #dimension etc.
	8
	9 while not converge
	10  #depend on l1 or l2 norm is used
	11 	para_rdd = data_rdd.MapPartitions(SGD(using sklearn))
	12	average all the parameters learnt by SGD
	
The pseudo-code is very very simple. But it cost me a lot of time to make this work on billions instances. Based on some following experience, LR can handle billions-dataset on a cluster with 240 cpu cores and 640 GB memory in total. However, the disk space is also a bottleneck that I will metion later.


##Tips and experiences:

**Line 1**: repartition() function in pyspark results in a more balance partitions. However, repartition requires too much computation, memory as well as disk for shuffle. After several attempts, I will never utilize repartition() directly on such large dataset.

**Line 3**: Maybe particular for python using scipy.sparse package. Building csr_matrix is quite expensive. Thus, instead of building csr_matrix for each instance again and again. We will directly map each partition to a big csr_matrix. 

**Line 6**: Converting the large dataset to a big csr_matrix run out of memory several times as well. Thus, in the final version code, I serialize to building several smaller csr_matrix and concat in the last. This will trade some time for memory. But I believe it is worth as you cannot guarantee how large the dataset will be. 

Storage.MEMORY_AND_DISK is suggested in my opinion to persist. Intuitively, this results in crazy usage of disk space. However, compared to the usage by shuffle metioned later, this is acceptable.

**Line 11**: I just call sklearn.linear_model.SGDClassifier to do SGD in each partitions. No doubt that you can implement one yourself which should be more fun. 

One of biggest challenge here is that the high-dimension(10e8) parameters vectors obtained from each partitions has to be averaged. Calling sum(), reduce() lead to calling a collect(). This means, in my experiment, collecting 100GB sparse vector back to master. Obviously, this is not acceptable. As a result, for $$$w_i$$$ obtain in partition $$$i$$$, I partition $$$w_i$$$ to #parallesim. For instance $$$w_i \rightarrow (1,w\_{i,1}), (2,w\_{i,2})\dots(k,w\_{i,k})$$$. $$$k$$$ denotes the k which is identical for all the partitions. Afterwards, reduceByKey is called to sum up all the resul and only one parameter vector is collected back.

Furthermore, a serious side effect is that we change the key in doing the above trick. And each time, for instance, 100GB(400 partitions * 300MB sparse vector) hash to be shuffled and write to disk. For really many times, my disk is running out. I try to compress the shuffle by flush the shuffle files to hdfs. But both does not work well. 

No doubt that fewer partition will alleviate this problems. However, few partitions means that you have to use fewer cpus to avoid the memory is running out. Quite several time have to be attempted.

In total, to avoid keeping all the dataset in memory, I follows the guidance in [blog of Alex Smola][4] that 

> We overpartition the dataset and using a fixed learning rate for SGD.

This is the mechanism I implements, the majority of time is costed on tricks and debugging. I have no idea how to test and dubug when the problems can only occur when large dataset.

Moreover, I would be appreciated if you can offer me some discussion or hints caused, currently, the disk usage, memory usage and cpu usage is not perfect. Only very few cpus are used for memory concerne. Moreover, if you can inspire me to avoid the shuffling of realling huge data of parameters vectors. I will also be appreciated.


[1]: http://en.wikipedia.org/wiki/Logistic_regression
[2]: http://en.wikipedia.org/wiki/Stochastic_gradient_descent
[3]:https://spark.apache.org/
[4]:http://blog.smola.org/post/977927287/parallel-stochastic-gradient-descent