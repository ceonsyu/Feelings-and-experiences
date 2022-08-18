## Learning Tree-based Deep Model for Recommender System
- Predicting user interests from coarse to fine by traversing tree nodes in a top-down fashion and making decisions for each **user-node** pair.
- Each node of the tree except the root node has one parent and an arbitrary number of children.
- Each item $c_i$ in the corpus $C$ corresponds to one and only one **leaf node**.
- Those non-leaf nodes are **coarse-grained** concepts.

### Usage of the tree
Searching topK interesting items for each user. In the retrieval process, each layer keeps K nodes and extends them. The key problem is how to get the accurate interest discriminator in each layer, to find the K most interested nodes in each layer.

### Discriminator
Deep model plays the role of discriminator in TDM, whose outputs are the interest of (user, node) pairs.

### Example 
Official [quick start](https://github.com/alibaba/x-deeplearning/wiki/%E6%B7%B1%E5%BA%A6%E6%A0%91%E5%8C%B9%E9%85%8D%E6%A8%A1%E5%9E%8B(TDM)). Docker, [hadoop](https://medium.com/beeranddiapers/installing-hadoop-on-mac-a9a3649dbc4d), siwg, cmake are needed.
There are some problems during trying the example:
- Hadoop is needed, but it's hard to install. [This guide](https://zhuanlan.zhihu.com/p/59758201) is good but there still many problems.
```shell
root@h01:/usr/local/hadoop/bin# hdfs namenode -format
WARNING: HADOOP_PREFIX has been replaced by HADOOP_HOME. Using value of HADOOP_PREFIX.
Error: Could not find or load main class org.apache.hadoop.hdfs.server.namenode.NameNode

root@h01:/usr/local/hadoop/sbin# ./start-all.sh
WARNING: HADOOP_PREFIX has been replaced by HADOOP_HOME. Using value of HADOOP_PREFIX.
WARNING: HADOOP_PREFIX has been replaced by HADOOP_HOME. Using value of HADOOP_PREFIX.
Starting namenodes on [h01]
WARNING: HADOOP_PREFIX has been replaced by HADOOP_HOME. Using value of HADOOP_PREFIX.
h01: ERROR: Cannot set priority of namenode process 5062
```
- [xdl](https://github.com/alibaba/x-deeplearning/wiki/%E7%BC%96%E8%AF%91%E5%AE%89%E8%A3%85) is needed, but somehow python script can't import it.
- `cmake` process has some problems, can't find this and can't find that, it's a mess.