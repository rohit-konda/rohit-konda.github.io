---
title: Optimal Stopping Theory
tags: [Operations Research]
style: 
color: 
description: We give a brief overview of optimal stopping problems and it's relevance to market design.
---


![Car Salesman Problem](figs/optimal-stopping/market.svg)

## How to be a Good Car Salesman
Let's say that you put your car on the market and line of willing customers forms to buy your car. Each buyer has a purchase price that they are willing to spend; however this information is not available to you. When a customer is at the front of the line, you have the option of accepting the price that the customer offers, or to reject their offer and move on to the next customer. All rejected customers leave the market permanently and if you accept the offer, then the car is sold to that customer for their bargaining price. Now the question is, *how should you go about selling the car?* Accepting too early means missing out on future potential customers, but accepting too late means missing out on previous customers.

We answer these questions through the field *Optimal Stopping Theory*. 

## Optimal Stopping Problems

The theory of optimal stopping involves choosing a time to stop a stochastic process to maximize the reward that is dependent on a given reward function and a realization. Formally, these problems are defined by two things:

- A sequence of random variables - $X_1, X_2, \dots $  with known joint distributions
- A series of rewards - $y_1(x_1), y_2(x_1, x_2) \dots$ with known reward functiosn and realizations $x_i \sim X_i$.

The problem is to define a stopping rule in which we maximize the expected profit
$$
\text{Profit} \doteq \max_{t} \mathbb{E}[y_t(\{x_i\}_{i \leq t})].
$$

There are many applications of this problem including applications in optimal control theory, event-triggered systems and switch systems. Other applications include investment strategies and hypothesis testing. Some interesting examples of optimal stopping problems are given below according to.

### Maximizing Heads
You observe a fair coin being tossed repeatedly and you can stop the process any time. The question is *when should you stop the process to maximize the average number of heads that show up in the sequence?* To find this, you need to know the optimal stopping rule and the corresponding guarantees. If the first coin toss is heads, you should stop immediately to get a reward of $1$. On the other hand, if the average is ever below $1/2$ at a certain point, you can always wait long enough for the average to get back up to $1/2$ due to the law of large numbers. In fact, there is a stopping rule that achieves an expected payoff of $.79$ for the average of heads in the sequence!

### One Arm Bandit Problem
Let there be two treatments for a disease, an experimental treatment **A**, in which the probability of success $p_A$ is not known and the standard or established treatment **B**, where the probability of success $p_B$ is known. You have a group of patients that are treated sequentially, and you would like to decide which treatment to give them to maximize the number of patients cured. You can only figure out the $p_A$ based on the response by previous patients in the sequence. If it is ever determined that $p_A \leq p_B$, then you should switch to treatment **B** for the rest of the patients (similarly in the other direction). Therefore, this problem can be formulated as an optimal stopping problem.

## Prophet Inequalities

## Secretary Problems 

These problems are similar to prophet problems but consider the following scenario. There are $n$ distinct non-negative variables whose ranges are unknown. The items are presented to us one by one and we have to decide whether to accept the item or reject it for the next item in the sequence. The goal is to maximize the probability that we choose the highest valued item.

If the order is picked adversarially, then every deterministic strategy fails, and randomizing gives us a probability guarantee $\frac{1}{n}$, which cannot be improved. Therefore, we consider the case where the items are presented in a uniformly random order. 

In this case the best strategy can guarantee a probability of $\frac{1}{e} \sim .37$ of choosing the maximum valued item. We review a simple strategy gives a probability guarantee of at least $\frac{1}{4}$. Ignore the first $n/2$ items and pick the next item that is larger than all the items in the first half. The probability of choosing the largest item using this strategy is lower bounded by the probability of the largest item being in the second half and the second largest item being in the first half.






> wef.  
> wef.  
> wer.  

```python
for i in range(10):
    print('this is cool.')
```


<details>
  <summary>Click to expand</summary>
  This is the hidden content that appears when you click the summary.

  Inline math: $E = mc^2$

  Block math:
  $$
  E = mc^2
  $$
</details>


### Theorem 1 (Pythagorean Theorem)
For a right-angled triangle with sides \( a \) and \( b \), and hypotenuse \( c \), the following holds:

$$
a^2 + b^2 = c^2
$$

**Proof:**  
Consider a right triangle with legs \( a \) and \( b \) and hypotenuse \( c \). By constructing two identical triangles and rearranging them into a square, we derive:

$
c^2 = a^2 + b^2
$

Thus, the theorem is proven $\square$.