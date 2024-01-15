# Exercises from Reinforcement Learning: An Introduction

## Chapter 1

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

## Chapter 2

### Exercise 2.1

0.5+(1-0.5)*0.5 = 0.75

### Exercise 2.2: Bandit example

$ Q_1(1) = -1 \implies A_2=2 $
$ R_2=1 \implies Q_2(2) = 1 \implies A_3=2 $
$ R_3=-2 \implies Q_3(2) = -0.5 \implies A_4=3 $

But $A_4=2$, thus $\epsilon$ case occured.

$ R_4=2 \implies Q_4(2) = 0.5 \implies A_5=2 $

But $A_5=3$, thus $\epsilon$ case occured.

In all, in time step 4 and 5, $\epsilon$ case definitely occured, and in other time steps, $\epsilon$ case could possibly have occured but accidentally chose the best one.

### Exercise 2.3

In the long run, we assume that all the $Q$ values have converged to $q_*$, so we have found the best action. We also assume that the reward converges to coresponding $q_*$ values, which is equal for both cases. So for $\epsilon=0.01$, there is 99.1% chance of choosing the best action, which is 91% for $\epsilon=0.1$. We can know that for the outcome of both average reward and percentage of optimal action, $\epsilon=0.01$ will be higher by:

$$
\frac{99.1\%-91\%}{91\%}\times 100\%=8.9\%
$$

### Exercise 2.4

$$
\begin{align*}
Q_{n+1} &= Q_n + \alpha_n[R_n-Q_n] \\
 &= (1-\alpha_n)Q_n + \alpha_nR_n \\
 &= (1-\alpha_n)[(1-\alpha_{n-1})Q_{n-1} + \alpha_{n-1}R_{n-1}] + \alpha_nR_n \\
 &= \cdots \\
 &= (1-\alpha_n)(1-\alpha_{n-1})\cdots (1-\alpha_1)Q_1 \\ &\quad + \sum_{i=1}^{n}(1-\alpha_n)(1-\alpha_{n-1})\cdots (1-\alpha_{i+1})\alpha_iR_i \\
 &= \prod_{i=1}^n(1-\alpha_{i})Q_1 + \sum_{i=1}^{n}[\prod_{j=i+1}^n(1-\alpha_j)]\alpha_iR_i
\end{align*}
$$



### Exercise 2.5

The trial is taken in file://./jnote/exercise2-5.ipynb.
From the results, I learned that the sample-average method does face difficulties for nonstationary models. I think the reason is that for a nonstationary model, a newer reward is always more important than an older reward, which means we cannot treat them as the same. With a constant factor, we give the newer rewards more value.

### Exercise 2.6: Mysterious Spikes

Because in early times, the agent is actively exploring different actions. So I think if it chose the best option in accident, it will get a high rise. But quickly it turns to another option which may be bad, and the result drops again, leaving a spike in the plot.

### Exercise 2.7: Unbiased Constant-Step-Size Trick

$$
\begin{align*}
\bar o_n=\frac{\alpha}{\beta_n}&=\bar o_{n-1}+\alpha(1-\bar o_{n-1}) \\
\frac{1}{\beta_n}&=\frac{1}{\beta_{n-1}}+(1-\frac{\alpha}{\beta_{n-1}}) \\
1-\beta_n&=\frac{1-\alpha}{(1-\beta_{n-1})-\alpha}
\end{align*}
$$

$$
\begin{equation*}
\bar o_1 = \bar o_0+\alpha(1-\bar o_0)=\alpha
\implies\beta_1 =\frac{\alpha}{\bar o_1}=1
\implies 1-\beta_1=0
\end{equation*}
$$

$$
\begin{align*}
\implies Q_{n+1} &= Q_n + \beta_n[R_n-Q_n] \\
 &= (1-\beta_n)(1-\beta_{n-1})\cdots (1-\beta_1)Q_1 \\ &\quad + \sum_{i=1}^{n}(1-\beta_n)(1-\beta_{n-1})\cdots (1-\beta_{i+1})\beta_iR_i \\
 &=\sum_{i=1}^{n}(1-\beta_n)(1-\beta_{n-1})\cdots (1-\beta_{i+1})\beta_iR_i
\end{align*}
$$

So the estimation is now unbiased.

### Exercise 2.8: UCB Spikes (?)

Like in Exercise 2.6, I think exploration usually bring spikes: the agent accidentally hits the best choice, and then leave to take the next exploration, which causes a spike. 

### Exercise 2.9

$$
\begin{align*}
\pi_t(1) &= \frac{e^{H_t(1)}}{e^{H_t(1)}+e^{H_t(2)}} \\
&= \frac{1}{1+e^{H_t(2)-H_t(1)}} \\
&= \frac{1}{1+e^{-[H_t(1)-H_t(2)]}}
\end{align*}
$$


, which is a sigmoid function ${\rm sigmoid}(x)=\dfrac{1}{1+e^{-x}} $ , where $x=H_t(1)-H_t(2)$, and similarly for $\pi_t(2)$.

### Exercise 2.10

a) If take action 1: E[R] = 0.1\*0.5+0.9\*0.5=0.5. If take action 2: E[R] = 0.2\*0.5+0.8\*0.5=0.5
Both the same, sowe can take either each time.
b) In case A, always choose action 2. In case B, always choose action 1. E[R] = 0.2\*0.5+0.9\*0.5=0.55

### Exercise 2.11 (programming)

See file://jnote/exercise2-11.ipynb

I found that in nonstationary situation, eps-greedy remains its performance, while other algorithms got worse performance, and the relationship between average reward and coresponding parameters is also different.
