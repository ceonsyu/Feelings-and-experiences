## COLD(Computing power cost-aware Online and Lightweight Deep pre-ranking system)
Key features of COLD:
- In ali's real system, COLD model is a seven-layered fully connected deep neural network with SE(Squeeze-and-Excitation) block. 
- Computing power cost is explicitly reduced by applying optimization tricks such as parallel computation and semi-precision calculation for inference acceleration.
- COLD model works in an online learning and severing manner, bringing system ability to handle the challenge of data distribution shift.
### Details
COLD designers apply two ways of optimization strategy: one way is to design a **flexible network architecture** that can make a trade-off between model performance and computing power cost, the other way is to reduce computing power cost by applying **engineered optimization tricks** for inference acceleration.
#### Flexible Network Architecture
There are many ways to get a lightweight version of the deep model from the full version of the initial model, such as network pruning, feature selection, and neural architecture search. The COLD designers choose the **feature selection**. Specifically, they apply the SE block for feature selection, by getting the **importance weights** of group-wise features and select the most suitable ones.
#### Engineered Optimization Tricks
- Parallelism at all level. 
- Column based computation.
- Low precision GPU calculation.

In general, COLD achieved the goal of using the cross features of user features and ad features in the pre-ranking system, with the computing performance and the reducing of computation power acceptable.
![development history of the pre-ranking system](figures/截屏2022-08-09%20下午6.17.38.png)

