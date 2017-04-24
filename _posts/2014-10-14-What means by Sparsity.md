---
layout: post
title: What mean by sparsity?
modified: 2014-10-14
tags: [survey, sparsity]
---

What mean by sparsity?

In machine learning area, we hear a lot about sparsity such as compressed sensing, sparse coding, data sparsity and so on. Amongst, I am particular interested in data sparsity. In recommender system, the large proportion of missing ratings is called sparsity. On the other hand, the bag of word(BoG) represented document dataset is also named sparse data. What exactly means by sparsity is the fundamental problem for us to understand as well as utilize data sparsity. My original confusion is posted on [Cross Validated][1].

In this blog, I hope to list the taxonomy and several definition from very intuitive perspective. Moreover, I would like to emphasize that this blog only talks about sparse data instead of sparse learning. The object method aims at learning a sparse parameter.

First of all, I want to clarify two types of data sparsity[^1].

1. Paucity of dataset particular training data.
2. High dimension feature space and only few dimensions are informative for each instance.

**Paucity of training data**: Take the [Netflix Prize][2] dataset as example again. The large proportion of missing ratings makes recovering the user-movie matrix more challenging. The sparsity ratio, $$\frac{\#observerd}{\# user \times \# movies}$$, is always utilized how sparse the dataset is. Lee, J[^2] provides an empirical analysis the relation between performance and density/sparisty. The insufficient training data situaiton is quite common.

**High dimension feature space**: Take the linear classifier for binary classification as example. As we known, the VC dimension of linear classifier is $$O(d)$$ where $$d$$ is feature dimension. As the dimension increase, the number of instance is required to grow as well.

The high dimensionality also results in some other problems known as **curse of dimensionality**. The sparsity is only one of consequences of curse of dimension. The distance becomes meaningless as dimension increase. However, the discusion of curse of dimension is beyond this post.

In text mining, bag of word is always utilized to represent each domument like the following.

\\[[0,1,0,0,0\dots,0,0,0,\dots,1,0,\dots]\\]

We usually call such instance sparse caused only few entries are non-zero. However, such understanding is quite on the surface. As I actually cannot explain the difference between $$[0,1,0,0,1]$$ and $$[1,2,1,1,2]$.$$ However, the latter one will not be called sparse. Duchi, J.[^3] provides a formal condition for sparse as
\\[\text{for convex loss function } f,supp(f) \subset supp(\nabla f)\\]

From intuitive perspective, such condition means that the $$i\_{th}$$ of instance dimension $$x$$ is zero $$x_i=0$$, then the gradient with respect to $$x_i$$ is deemed to be zero. Consider using stochastic gradient descent to learn the model. The instance with sparse features $x_i=0$ will not update $$i\_{th}$$ dimension at all. Duchi,

J.[^3] also provides an analysis of stochastic optimization on such sparse data. When learning on such sparse dataset, we would like to learn an dense model rather than sparse model(assumption). Such assmption leads much harder to learn model on sparse data.

**Other definition**

At the very begining of my survey. I always try to make an uniform definition for the above two type of sparsity. Actually, there indeed exist some common parts.

1. Both the paucity of training data and high dimension will cause the average distance between each data point large.
2. The [sample density][3] is also tried to measure the sparsity.

In the following, I try to quote several "definition" in other references.

1. Data sparsity refers to the difficulty in finding sufficient reliable similar users since in general the active users only rated a small portion of items[^5]
2. data sparsity problem occus in the setting of supervised statistical learning method, when some data from the test side is not present in the training dataset. [^6]
3. when the training data is relatively sparse in this domain, either because few observations are available for learning or because the underlying structure is complex, the bias inherent in popular pruning methods is inappropriate and they have a negative effect on predictive accuracy[^4].
4. One way to think of sparsity is how space is empty (60%), whereas 40% of space is dense, or filled. So good data looks like swiss cheese.  Big bubbles of nothing[^7]!

There exist quite a lot definition or understanding of data sparsity. As far as I have survied, I do not find a very persuasive and comprehensive work to clarify all of these definitions.


[1]: http://stats.stackexchange.com/questions/113318/the-name-data-sparsity-in-different-applications "Cross Validated"
[2]: http://en.wikipedia.org/wiki/Netflix_Prize
[3]:http://math.stackexchange.com/questions/283006/what-is-a-sampling-density-why-is-the-sampling-density-proportional-to-n-fra


##References


[^1]: David Donoho, Sparsity in Modern High-Dimensional Statistics, SAMSI Astrostatistics. 20,9,2012
[^2]: Lee, J., Sun, M., & Lebanon, G. (2012). A comparative study of collaborative filtering algorithms. arXiv preprint arXiv:1205.3193.
[^3]: Duchi, J., Jordan, M., & McMahan, B. (2013). Estimation, optimization, and parallelism when data is sparse. In Advances in Neural Information Processing Systems (pp. 2832-2840).
[^4]: when the training data is relatively sparse in this domain, either because few observations are available for learning or because the underlying structure is complex, the bias inherent in popular pruning methods is inappropriate and they have a negative effect on predictive accuracy.
[^5]: Guo, G. (2013, August). Improving the performance of recommender systems by alleviating the data sparsity and cold start problems. In Proceedings of the Twenty-Third international joint conference on Artificial Intelligence (pp. 3217-3218). AAAI Press.
[^6]: Ricci, F., Rokach, L., & Shapira, B. (2011). Introduction to recommender systems handbook (pp. 1-35). Springer US.
[^7]: http://www.quora.com/What-is-a-clear-explanation-of-data-sparsity
