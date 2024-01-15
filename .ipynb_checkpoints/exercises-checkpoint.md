# 强化学习导论 练习题

## 第一章

### Exercise 1.1: Self-Play
In self-play, there are two agents learning in parallel, so both of them may continuously updating their policies. Possibly, they can converge into a Nash equilibrium， which means no one can win by improving themselves, then they may have learned the optimal policy.
### Exercise 1.2: Symmetries
a) We can treat positions with symmetry as the same state, thus we can reduce the number of states.
b) No. Because the opponent did not take advantage of symmetries, which means for different positions with symmetry, the opponent may take different action, so those positions should be different states.
### Exercise 1.3: Greedy Play
I think it will be worse. Because the prior settings of the rates are arbitrary, the player need to improve the accuracy by exploring unseen actions, which may lead to failure. And a greedy player will never take this risk. The lack of exploration may cause the problems of falling into local optimum or overfitting.
### Exercise 1.4: Learning from Exploration (?)
If not learning from explotary moves, the values may converge to the winning percentage of the best policy. If learning from explotary moves, the values may converge to the winning percentage of a second best policy.
### Exercise 1.5: Other Improvements

## 第二章

### Exercise 2.1

0.5+(1-0.5)*0.5 = 0.75

### Exercise 2.2: Bandit example

$ Q_1(1) = -1 \implies A_2=2 $
$ R_2=1 \implies Q_2(2) = 1 \implies A_3=2 $
$ R_3=-2 \implies Q_3(2) = -0.5 \implies A_4=3 $

But $A_4=2$, thus $\epsilon$ case occured.

$ R_4=2 \implies Q_4(2) = 0.5 \implies A_5=2 $

But $A_5=3$, thus $\epsilon$ case occured.

In all, in time step 4 and 5, $\epsilon$ case definitely occured, and in other time steps, $\epsilon$ case could possibly have occured.

### Exercise 2.3

In the long run, we assume that all the $Q$ values have converged to $q_*$, so we have found the best action. We also assume that the reward converges to coresponding $q_*$ values, which is equal for both cases. So for $\epsilon=0.01$, there is 99.1% chance of choosing the best action, which is 91% for $\epsilon=0.1$. We can know that for the outcome of both average reward and percentage of optimal action, $\epsilon=0.01$ will be higher by:
$$ \frac{99.1\%-91\%}{91\%}\times 100\%=8.9\% $$

### Exercise 2.4

$$ \begin{align*}
Q_{n+1} &= Q_n + \alpha_n[R_n-Q_n] \\
        &= (1-\alpha_n)Q_n + \alpha_nR_n \\
        &= (1-\alpha_n)[(1-\alpha_{n-1})Q_{n-1} + \alpha_{n-1}R_{n-1}] + \alpha_nR_n \\
        &= \cdots \\
        &= \prod_{i=1}^n(1-\alpha_{i})Q_1 +  \sum_{i=1}^{n}[\prod_{j=i+1}^n(1-\alpha_j)]\alpha_iR_i
\end{align*} $$

### Exercise 2.5

