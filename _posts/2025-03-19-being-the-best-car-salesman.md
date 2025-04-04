---
title: Being the Best Car Salesman
tags: [Operations Research]
style: 
color: 
description: We give a brief overview of optimal stopping problems and it's relevance to market design.
---


![Car Salesman Problem](/assets/images/optimal-stopping/market.svg)

## How to be a Good Car Salesman?
Let's say that you put your car on the market and line of willing customers forms to buy your car. Each buyer has a purchase price that they are willing to spend; however, this information is not available to you. When a customer is at the front of the line, you have the option of either 1. accepting the purchase price that the customer offers, or 2. to reject their offer and move on to the next customer. All rejected customers leave the market permanently. If you accept a customer's offer, then the car is sold to that customer for their purchase price. Now the question is, *how should you go about selling the car?* Accepting an offer too early may mean missing out on future customers with a higher purchase price, but aggresive rejection may force accepting a lower offer later down the line. 

We explore this trade-off through the field of *Optimal Stopping Theory*. 

## Optimal Stopping Problems

The theory of optimal stopping involves choosing a time to stop a stochastic process to maximize the reward that is dependent on a given reward function and a realization. Formally, these problems are defined by two things:

- A sequence of random variables - $X_1, X_2, \dots $  with known joint distributions
- A series of rewards - $y_1(x_1), y_2(x_1, x_2) \dots$ with known reward functions and realizations $x_i \sim X_i$.

The problem is to define a stopping rule in which we maximize the expected profit

$$
\text{Profit} \doteq \max_{t} \mathbb{E}[y_t(\{x_i\}_{i \leq t})].
$$

There are many applications of this problem including applications in optimal control theory, event-triggered systems and switch systems [(Karatzas 1984)](https://epubs.siam.org/doi/pdf/10.1137/0322054?casa_token=gnJrmcVlLR0AAAAA:ED-ywCViEeuPojrBoHVpvgdZGeNkqj57WbsS8_KdZnGmsxVTsYf8Hmn_Ha8aTXz7WVMzjny7jBs "Connections between optimal stopping and singular stochastic control I. Monotone follower problems"). Other applications include investment strategies and hypothesis testing. Some interesting examples of optimal stopping problems are given below according to [(Ferguson 2006)](https://www.math.ucla.edu/~tom/Stopping/Contents.html "Optimal Stopping and Applications").

### Maximizing Heads
You observe a fair coin being tossed repeatedly and you can stop the process any time. The question is *when should you stop the process to maximize the average number of heads that show up in the sequence?* To find this, you need to know the optimal stopping rule and the corresponding guarantees. If the first coin toss is heads, you should stop immediately to get a reward of $1$. On the other hand, if the average is ever below $1/2$ at a certain point, you can always wait long enough for the average to get back up to $1/2$ due to the law of large numbers. In fact, there is a stopping rule that achieves an expected payoff of $.79$ for the average of heads in the sequence!

### One Arm Bandit Problem
Let there be two treatments for a disease, an experimental treatment **A**, in which the probability of success $p_A$ is not known and the standard or established treatment **B**, where the probability of success $p_B$ is known. You have a group of patients that are treated sequentially, and you would like to decide which treatment to give them to maximize the number of patients cured. You can only figure out the $p_A$ based on the response by previous patients in the sequence. If it is ever determined that $p_A \leq p_B$, then you should switch to treatment **B** for the rest of the patients (similarly in the other direction). Therefore, this problem can be formulated as an optimal stopping problem.

## Revisiting the Car Salesman Problem

Let's revisit the car salesman problem and make it a little more formal. Consider a set of $n$ buyers where each buyer's purchase price is a random variable $X_i$ for $i \in \\{1, \dots, n \\}$ (We remark that you don't know what order the customers will line up in). The distributions of each of the random variables is known to you (for example, you have some knowledge on the customer demand), but the exact purchase price realizations are not known to you.

The exact customer selection process is as follows. You begin the process, where $i = 1$ denotes the start of the line. At each step $i$ of the line, you are able to witness the $i$ th's customer's purchase price realization $x_i \sim X_i$. Again, you are able to either accept $x_i$ (the realized purchase price) or go on to the next customer $i+1$.

To assess the performance of the your decision strategy, we compare expected profit in comparison to the case where you knew all of the realizations $ \\{x_i\\}_{i \leq n}$ before hand (and not just the distributions $\\{X_i\\}_{i \leq n}$ ). In the case of full information, the profit is the maximum $\max_i x_i \sim X_{\max} \doteq \max(X_1, \dots, X_n)$. It was shown in the seminal paper in [(Krengel 1978)](https://projecteuclid.org/journalArticle/Download?urlid=bams%2F1183538915 "On semiamarts, amarts, and processes with finite value") that there exists a decision rule that can guarantee the expected payoff of $\frac{1}{2} \mathbb{E}[X_{\max}]$. In fact, no other customer selection strategy can do better, by the following example. 


#### Example.
Let there be two customers with the purchase price $X_1 = 1$ with full probability and $X_2 = \frac{1}{\varepsilon}$ for some probability $0 < \varepsilon \ll 1$ and $0$ otherwise. A car salesman can either pick customer 1 or customer 2 and get an expected payoff of $1$. If you as the car salesman knows the realizations, you can guarantee a payoff of $\mathbb{E}[X_{\max}] = P(x_1 \geq x_2) \cdot \frac{1}{\varepsilon} +  P(x_2 \geq x_1) \cdot 1 = 2 - \varepsilon$. The your strategy does not matter in this scenario - if you doesn't know the purchase price realizations, you are forced to incur the $\frac{1}{2}$ factor penalty.

### A Simple Optimal Strategy

Let's dispense with the suspense and finally discuss the optimal strategy as a car salesman. In fact, the optimal strategy is a **fixed price mechanism**! This is shown as a *prophet inequality* in ([Correa 2017](https://dl.acm.org/doi/pdf/10.1145/3033274.3085137?casa_token=z8OTTHJQSlQAAAAA:gEQPBy311IJaRIRbJlANJP7-pu6AsMF-V17R5sAVsu32ezcRIMGCu3ZIcpD3fTc9DTARa1jWhUytyQ "Posted Price Mechanisms for a Random Stream of Customers")). In other words, you should set a sticker price, and accept the first customer whose purchase price realization is above that. The optimal sticker price actually corresponds to the median of the distribution $X_{\max}$ (which you can compute since you know the distributions $X_1, \dots, X_n$ ). If you know all the customers have the same purchase price distribution, the efficiency of this fixed price mechanism rises to $74.5\%$.

*Why is this interesting?* There are many different market designs, like trading or bartering or auctions. But there is a reason that fixed prices is predominantly used in stores - it is quick, easy, and apparently optimal in a theoretical sense as well! You can thank this result as the reason you don't have to barter in grocery stores.

<details>
  <summary>We give the proof of the optimality for the fixed price mechanism here.</summary>

Let $\mathbb{E}[X_\mathrm{alg}]$ denote the expected profit according to the fixed price algorithm at the median value. Then we have the following set of inequalities.
$$\mathbb{E}[X_\mathrm{alg}] = \mathbb{E}_i[\mathbb{E}[X_\mathrm{alg}| X_i \text{ is first item with value above } M]] \ + $$
$$ \mathbb{E}[X_\mathrm{alg} | X_{\max} \leq M] P(X_{\max} < M)  $$
$$ = \mathbb{E}_i[\mathbb{E}[X_i| X_i \text{ is first item with value above } M]] $$
$$ = \mathbb{E}_i[\mathbb{E}[X_i- M + M| X_i \text{ is first item with value above } M]] $$
$$ = M \cdot P(X_{\max} \geq M) + \mathbb{E}_i[\mathbb{E}[X_i - M| X_i \text{ is first item with value above } M]] $$
$$ = M \cdot P(X_{\max} \geq M) + \sum_{i=1}^{n} \mathbb{E}[X_i - M| X_i \geq M] \cdot P(\bigwedge_{j < i}X_j \leq M) P(X_i \geq M) $$
$$ = M \cdot P(X_{\max} \geq M) + \sum_{i=1}^{n} \mathbb{E}[(X_{i}-M)^+] \cdot P(\bigwedge_{j < i}X_j \leq M) $$
$$ \geq M \cdot P(X_{\max} \geq \mathrm{M}) + \sum_{i=1}^{n} \mathbb{E}[(X_{i}-M)^+] \cdot P(X_{\max} \leq M) $$
$$ \geq M \cdot P(X_{\max} \geq \mathrm{M}) + \mathbb{E}[(X_{\max}-M)^+] \cdot P(X_{\max} \leq M) $$
$$ \geq \mathbb{E}[X_{\max}]/2.$$

Here we use the notation $\mathbb{E}[(X_{i}-M)^+] \equiv \mathbb{E}[\max\{X_{i}-M, 0\}]$. Note that

$$ \mathbb{E}[(X_{i}-M)^+] = \mathbb{E}[(X_{i}-M)^+ | X_i \leq M] P(X_i \leq M) \ + $$
$$ \mathbb{E}[(X_{i}-M)^+ | X_i \geq M] P(X_i \geq M) $$
$$ = \mathbb{E}[X_{i}-M | X_i \geq M] P(X_i \geq M). $$
</details>
