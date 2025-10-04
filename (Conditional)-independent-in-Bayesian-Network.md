# 1. Bayesian Network

Bayesian Network(**BN**) is composed of Directed Acyclic Graph (**DAG**) and Conditional Probability Tables (**CPT**)

In the DAG, nodes means events, edges means sequences between nodes. Each event happens(or not happens) with conditional probability $\mathbb{P}$, where the conditional probability is given by CPT.

> Why conditional probability in CPT ?

Because in Bayesian Network, events happen sequentially. The sequence of nodes implies the sequence of events. When building the BN, an event can only be observed after observing its parents (happen or not happen), which means every event probability (except the sources) in CPT is conditional probability. (But we can observe events _after_ the BN is completed)

One can think CPT as prior knowledge, the probabilities in it might change if we have more observations.

_Example_  
A simple BN with DAG:

```
A --> B
```

and CPT:

| $P(A)$      | $P(B \mid A)$      |
| ----------- | ------------------ |
| $P(\neg A)$ | $P(B \mid\neg A)$  |
|             | $P(\neg B \mid A)$ |
|             | $P(\neg B \mid A)$ |


We can not get ${P}(B)$ directly from CPTs, but we can calculate it using Bayes’ Rule and Law of total probability

$$\begin{aligned} P(B) & =\sum_i P\left(B A_i\right) \\ & =P(B \neg A)+P(B A) \\ & =P(B \mid \neg A) P(\neg A)+P(B \mid A) P(A)\end{aligned}$$

# 2. Independent or conditional independent?

Mathematically, two event $A, B$ are independent iff $P(A | B)=P(A)$. Intuitively speaking, independent means the change of one event probability doesn’t affect another.

For example, originally we have $P(A)=0.5, P(B)=0.5$. Then something happened, $P(B)=0.9$. Because $A$ and $B$ are independent, $P(A)$ is not affected by the change of $P(B)$, still $P(A)=0.5$.

## Case 1

Given a BN with DAG:

```
A --> B
```

and CPT:

| $P(A)$      | $P(B \mid A)$      |
| ----------- | ------------------ |
| $P(\neg A)$ | $P(B \mid\neg A)$  |
|             | $P(\neg B \mid A)$ |
|             | $P(\neg B \mid A)$ |

> Are events $A$ and $B$ independent or not? Or, is $P(B)$ affected by the change of $P(A)$?

For $P(B)$, by Bayes’ Rule and Law of total probability:

$$P(B)=P(B \mid \neg A) P(\neg A)+P(B \mid A) P(A)$$

We can find $P(B | \neg A)$ and $P(B | A)$ from CPT, but we need $P(A)$ to calculate $P(B)$, which means the change of $P(A)$ affects $P(B)$.

Similarly argument for $P(A)$ as independence is symmetric.

So $A$ and $B$ are not independent.

## Case 2

Given a BN with DAG:

```
A --> B --> C
```

and CPT:


| $P(A)$      | $P(B \mid A)$           | $P(C \mid B)$          |
| ----------- | ----------------------- | ---------------------- |
| $P(\neg A)$ | $P(B \mid \neg A)$      | $P(C \mid \neg B)$     |
|             | $P(\neg B \mid A)$      | $P(\neg C \mid B)$     |
|             | $P(\neg B \mid \neg A)$ | $P(\neg C \mid\neg B)$ |

> Are $A$ and $C$ independent or not? Or, is $P(C)$ affected by the change of $P(A)$?

For $P(C)$, by Bayes’ Rule and Law of total probability:

$$\begin{aligned} P(C) & =\sum_i P\left(C B_i\right) \\ & =P(C \neg B)+P(C B) \\ & =P(C \mid \neg B) P(\neg B)+P(C \mid B) P(B)\end{aligned}$$

But we don’t know $P(B)$ yet. So using Bayes’ Rule and Law of total probability again:

$$\begin{aligned} P(B) & =\sum_i P\left(B A_i\right) \\ & =P(B \neg A)+P(B A) \\ & =P(B \mid \neg A) P(\neg A)+P(B \mid A) P(A)\end{aligned}$$

The change of $P(A)$ leads to the change of $P(B)$ (because $A\ B$ are not independent), and thus leading to the change of $P(C)$ (because $B\ C$ are not independent).

So $A$ and $C$ are not independent.

> Are $A$ and $C$ independent or not given $B$? Or, is $P(C)$ affected by the change of $P(A)$ given $P(B)$?

We can think “Given $B$” as we _refresh_ the probability of $B$, which is different from the prior $P(B)$ calculated by CPT. (Loosely speaking, $P(B)$ is “fixed” after given)  
Now we can calculate $P(C)$ directly using

$$\begin{aligned} P(C) & =\sum_i P\left(C B_i\right) \\ & =P(C \neg B)+P(C B) \\ & =P(C \mid \neg B) P(\neg B)+P(C \mid B) P(B)\end{aligned}$$

where $P(B)$ and $P(\neg B)$ is given by assumption, $P(C|\neg B)$ and $P(C|B)$ can be found from CPT. So the change of $P(A)$ does not affect $P(C)$

So $A$ and $C$ independent given $B$. Formally we say $A$ and $C$ are _conditionally_ _independent_ given $B$

## Case 3

Given a BN with DAG:

```
A <-- B --> C
```

and CPT:

| $P(B)$      | $P(A \mid B)$           | $P(C \mid B)$           |
| ----------- | ----------------------- | ----------------------- |
| $P(\neg B)$ | $P(A \mid \neg B)$      | $P(C \mid \neg B)$      |
|             | $P(\neg A \mid B)$      | $P(\neg C \mid B)$      |
|             | $P(\neg A \mid \neg B)$ | $P(\neg C \mid \neg B)$ |

> Are $A$ and $C$ independent or not? Or, is $P(C)$ affected by the change of $P(A)$?

For $P(A)$, by Bayes’ Rule and Law of total probability:

$$\begin{aligned} P(A) & =\sum_i P\left(A B_i\right) \\ & =P(A \neg B)+P(A B) \\ & =P(A \mid \neg B) P(\neg B)+P(A \mid B) P(B)\end{aligned}$$

For $P(C)$, by Bayes’ Rule and Law of total probability:

$$\begin{aligned} P(C) & =\sum_i P\left(C B_i\right) \\ & =P(C \neg B)+P(C B) \\ & =P(C \mid \neg B) P(\neg B)+P(C \mid B) P(B)\end{aligned}$$

The change of $P(A)$ leads to the change of $P(B)$ (because $A$ and $B$ are not independent, also everything in table is no fixed currently, they are priors, and can be modified by further observation), and thus leading to the change of $P(C)$. So the change of $P(A)$ does affect $P(C)$

So $A$ and $C$ are not independent.

> Are **A** and **C** independent or not given **B**? Or, is **P(C)** affected by the change of **P(A)** given **P(B)**?

Now we know the (“fixed”)value of $P(B)$. We can calculate $P(A)$ (or $P(C)$) using $P(B)$ without hesitation. Intuitively, the impact of $A$ on $C$ was “blocked” by a known $B$.

So, $A$ and $C$ are _conditionally_ _independent_ given $B$

## Case 4

Given a BN with DAG:
```
A --> B <-- C
```

and CPT:

| $P(A)$      | $P(C)$      | $P(B \mid A C)$              |
| ----------- | ----------- | ---------------------------- |
| $P(\neg A)$ | $P(\neg C)$ | $P(B \mid\neg A C)$          |
|             |             | $P(B \mid A\neg C)$          |
|             |             | $P(B \mid\neg A\neg C)$      |
|             |             | $P(\neg B \mid A C)$         |
|             |             | $P(\neg B \mid\neg A C)$     |
|             |             | $P(\neg B \mid A\neg C)$     |
|             |             | $P(\neg B \mid\neg A\neg C)$ |

> Are **A** and $C$ independent or not? Or, is $P(C)$ affected by the change of $P(A)$?

Intuitively, $A$and $C$ are source nodes, means they are not affected directly by any other nodes, their incidences have no conditions. Also we can find $P(A)$ and $P(C)$ from CPT directly. The change of probability of one does not affect the other.

How about I use the argument in previous example: ‘$A$ and $B$ are not independent, $B$ and $C$ are not independent, so the change of $A$ affect $C$ ’?

The change of $P(A)$ can lead to the change of $P(B)$ indeed. But we don’t how the change of $P(B)$ would affect $P(C)$. In previous example, we have $P(C)=P(C|\neg B)P(\neg B)+P(C|B)P(B)$, where $P(C)$ can be _determined_ by $P(B)$ and CPT. But here, for $P(B)$, we have

$$\begin{aligned} P(B)= & \sum_i \sum_j P\left(B A_i C_j\right) \\ = & P(B A C)+P(B A \neg C)+P(B \neg A C)+P(B \neg A \neg C) \\ = & P(B \mid A C) P(A C)+P(B \mid A \neg C) P(A \neg C) \\ & +P(B \mid \neg A C) P(\neg A C)+P(B \mid \neg A \neg C) P(\neg A \neg C)\end{aligned}$$

$P(B)$ is _determined_ by CPT and the _joint probability distribution_ of $AC$, we can not calculate $P(B)$ simply by CPT and $P(A)$. Even if $P(A)$ changes, we don’t know how it will affect $P(B)$, therefore, we don’t know how it will affect $P(C)$.

So $A$ and $C$ are independent.

> Are $A$ and $C$ independent or not given $B$? Or, is $P(C)$ affected by the change of $P(A)$ given $P(B)$?

Now we know the value of $P(B)$ and it is “fixed”. $P(B)$ depends on $A$ and $C$. If we change $P(A)$, $P(C)$ would also be changed to keep the consistency of $P(B)$.

So$A$ and $C$ are not independent given $B$.

The node $B$ in structure $A\rightarrow B\leftarrow C$  is called collider

# 3. Summary

$A\rightarrow B$ , $A$ and $B$ are not independent.

$A\rightarrow B \rightarrow C$, $A$ and $C$ are not independent. $A$ and $C$ are _conditionally_ _independent_ given $B$

$A\leftarrow B\rightarrow C$, $A$ and $C$ are not independent. $A$ and $C$ are _conditionally_ _independent_ given $B$

$A\rightarrow B \leftarrow C$, $A$ and $C$ are independent. $A$ and $C$ are not independent given $B$

