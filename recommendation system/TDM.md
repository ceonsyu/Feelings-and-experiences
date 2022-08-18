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