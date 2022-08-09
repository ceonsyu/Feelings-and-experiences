One common architecture for recommendation system consists of the following components:
- candidate generation (or matching 召回)
- scoring (or ranking 排序)
- re-ranking (重排)
### candidate generation
In this first stage, the system starts from a potentially huge corpus and generates a much smaller subset of candidates. 
### scoring
Next, another model scores and ranks the candidates in order to select the set of items to display to the user. Since this model evaluates a relatively small subset of items, the system can use a more precise model relying on additional queries. 
### re-ranking
Finally, the system must take into account additional constrains for the final ranking. For example, the system removes items that the user explicitly disliked or boosts the score of fresher content.
With the development of recommendation technology, there are many improvements of the architecture above. Such as pre-ranking, which can be viewed as a connecting link between matching and ranking modules.
![Illustration of cascade architecture for industrial information retrieval system, from alibaba's COLD paper](figures/截屏2022-08-09%20下午5.03.25.png)