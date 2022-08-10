## COLD(Computing power cost-aware Online and Lightweight Deep pre-ranking system)
### Shortcomings of the vector-product based DNN model(Which COLD is intended to optimize):
1. The model expression ability is limited by the vector-product form, and can not utilize the **user-ad cross feature**.
2. The pre-calculation costs too much time, making it hard to be adapted to the **data distribution shift**.
3. The model update frequency is also affected by the system implementation.


### Key features of COLD:
- In ali's real system, COLD model is a seven-layered fully connected deep neural network with SE(Squeeze-and-Excitation) block, using **cross vectors**. 
- Computing power cost is explicitly reduced by applying optimization tricks such as parallel computation and semi-precision calculation for inference acceleration.
- COLD model works in an online learning and severing manner, bringing system ability to handle the challenge of data distribution shift.
### Details
To **apply deep rank models** with complex architecture. COLD designers apply two ways of optimization strategy: one way is to design a **flexible network architecture** that can make a trade-off between model performance and computing power cost, the other way is to reduce computing power cost by applying **engineered optimization tricks** for inference acceleration.
#### Flexible Network Architecture
There are many ways to get a lightweight version of the deep model from the full version of the initial model, such as network pruning, feature selection, and neural architecture search. The COLD designers choose the **feature selection**. Specifically, they apply the SE block for feature selection, by getting the **importance weights** of group-wise features and select the most suitable ones.
- Importance weight calculation
- Feature group selection


#### Engineered Optimization Tricks
- Parallelism at all level. 
  - Split user's query, each query handles parts of the ads.
  - Multi-thread processing is used for feature computation.
  - GPU acceleration.
- Column based computation, calculate the cross vectors.
- Low precision GPU calculation.
  - Use linear-log operator to transform Float32 numbers into a reasonable range.

In general, COLD achieved the goal of using the cross features of user features and ad features in the pre-ranking system, with the computing performance and the reducing of computation power acceptable.
![development history of the pre-ranking system](figures/截屏2022-08-09%20下午6.17.38.png)

#### Several questions:
- What's the specific steps of COLD? What does every block mean in its infrastructure? What is GwEN?
- Why COLD can be implemented under a fully online infrastructure?
- How does SE block work?
- Why vector-based DNN has those shortcomings?