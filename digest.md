## A New Dog Learns Old Tricks: RL Finds Classic Optimization Algorithms

Source: openreview.net/forum?id=rkluJ2R9KQ

### Introduction

The goal of this work is to find out whether RL is capable of solving classic combinatorial problems and what kind of
solution it tends to find. Will it be close to known theoretical solution?

### Problems

#### Input Length Independence

Most of ML models are tend to work with inputs of specific length, though the tasks we are interested in should be able to work
this arbitrary data length. This impose hard restrictions on training RL agent. 

Modern approaches to come up with this problem is to use recurrent nets or convolutional masks of finite size. 
However they have problems of propagating back over long sequences and large time complexity.

The overcome is to investigate online versions of combinatorial algorims, so that inputs are comming one by one
in small patches. The decision is making at each step based on current state of agent and current input. 
Also for many tasks there is a clear notion of reward for every single action.

#### Input distribution

ML models are fit by minimizing expected loss dunction (or maximizing expected quality score) over given data distribution,
relying on the fact that test data distribution will be the same. But in theoretical computer science (TCS) algorithm
is usually judged by its perfomance on the worst possible input (worst-case analysis).

To make agent to learn such solutions there are two main approaches:
1. **Universal Training Set.** This is a common way to prove lower bounds in TCS. The idea is to come
up with a distribution over inputs and show that no algorithm can perform better than some factor $\alpha > 0$ 
compared to the optimal solution, in expectation.
2. **High-Entropy Training Set.** In some cases, it may be difficult to find a universal training set
or the universal training set may admit algorithms which perform well on the training set while
performing poorly on all other instances. To alleviate this problem authors also proposed to incorporate
training sets that have high entropy.

### Optimization Problems and Solutions

#### AdWords problem
<img src="https://i.ibb.co/NFdt8zF/AdWords.png">

#### Knapsack problem
<img src="https://i.ibb.co/XxLPTg2/Knapsack.png">

#### Secretary problem
<img src="https://i.ibb.co/nMVK2x7/Secretary.png">

### Results

#### AdWords problem
The model learns to find the Balance strategy (Kalyanasundaram and Pruhs, 2000) for unweighted graphs, and the MSVV strategy (Mehta et al., 2007)

#### Knapsack problem
The model learns to find an optimal threshold on value per unit size to use to either accept or reject incoming items.

#### Secretary problem
The model learns the optimal "Wait-then-Pick" algorithm which samples the first 1/e fraction of the input stream and then picks the next item which is higher
than any seen before. It also finds the optimal time-dependent value-threshold algorithm
for i.i.d. input.

### Future work

