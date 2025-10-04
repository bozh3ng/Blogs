Also published in [Medium](https://medium.com/@andrew.b.zheng/thinkings-about-probability-a2be81d93f49)
# 1. Confusion

**Statement**: Toss a coin, the probability of getting a head is 0.5.

There are (at least) two common explanations about this statement, Frequentist and Bayesian.

In the Frequentist interpretation, probability is defined as the long-run tests and observations. So, if we believe the statement, and we toss the coin 100 times, we will get about 50 heads, may be 53 may be 45, but around 50. If we toss the coin many many times , let’s say A times, we will observe exactly A/2 heads.  
While Bayesian said, we don’t know about the probability at the beginning, we guess one (as prior). Let’s (tentative) believe the probability of getting a head is 1, it doesn’t matter whether the belief is right or wrong. Then we update it by more tests. We toss it again, we observe a tail, then the probability can not be 1, we update our belief (as posterior). We toss it again, we update, we toss again… If we toss and update many many times, the belief (as the result of Bayes’ theorem) is 0.5

They both intuitively make sense, but again, what it means if something happens with probability? If I was told I have probability 0.4 to pass an exam, and I can attend the exam only once, either I pass it or I don’t. What it means I can pass it with probability 0.4? There is no such thing as 0.4 of a diploma. I will take the exam anyway, and I either pass or fail, what is the difference to me between 0.9 and 0.1 probability of passing?
# 2. (Discrete) Probability

**Definition**: A finite probability space ($\Omega$ , $\mathbb{P}$) is a finite set $\Omega$  and its (probability) measure ℙ which satisfies
- $\mathbb{P}(\Omega)=1$
- $\forall A\in \Omega,\mathbb{P}\geq0$

Technically speaking, a probability space is a triple $(\Omega,\mathcal{A}, \mathbb{P})$ , we omit the sigma-algebra to avoid more confusions.

Loosely speaking, probability is a function which can map an element in a set to real number between 0 and 1.

Toss a coin, the probability of getting a head is 0.5, it means: We construct a set with all the cases of tossing a coin. One case is that we get a head. The probability we are discussing is a function that map the event “head case” to real number 0.5.  
I can pass an exam with probability 0.4, it means there exists a function, which can map the event “I pass the exam” to real number 0.4. It is no difference from mapping the event to 0.9, or mapping the event to 0.1. Mathematics is not always useful in reality.

# 3. Conditional Probability

Recall probability space $(\Omega, \mathbb{P})$ 

Given a subset $B\subset\Omega$  with $\mathbb{P}(B)\geq0$, We define a new measure $\mathbb{P}^B:B\rightarrow[0,1]$ by

$$
\mathbb{P}^B(\{\omega\})=\frac{\mathbb{P}(\{\omega\})}{\mathbb{P}(B)} \quad \text { for } \omega \in B
$$

$\omega$ is singleton on $B$, so each $\omega$ is disjoint with each other and $\bigcup\omega=B$ 

To prove $\mathbb{P}^B$  is a probability measure, we need to show $\mathbb{P}^B=1$ , but $\mathbb{P}^B$ has not been  defined yet because $\mathbb{P}^B$ only accept $\omega\in B$

By the definition of $\mathbb{P}^B$:
$$
\sum_{\omega \in B} \mathbb{P}^B(\{\omega\})=\sum_{\omega \in B} \frac{\mathbb{P}(\{\omega\})}{\mathbb{P}(B)}=\frac{\sum_{\omega \in B} \mathbb{P}(\{\omega\})}{\mathbb{P}(B)}
$$

By the property of measure, for disjoint subsets
$$
\mu(\bigcup \omega)=\sum \mu(\omega)
$$

$$
\sum_{\omega \in B} \mathbb{P}(\{\omega\})=\mathbb{P}(\bigcup\{\omega\})=\mathbb{P}(B)
$$
$$
\sum_{\omega \in B} \mathbb{P}^B(\{\omega\})=\frac{\mathbb{P}(B)}{\mathbb{P}(B)}=1=\mathbb{P}^B(B)
$$

So $\mathbb{P}^B$ is a probability measure defined on $B$. $(B,\mathbb{P}^B)$ is a probability space.

By the countable subadditivity for disjoint subsets. For any event $A\subset B$ , we have:
$$
\mathbb{P}^B(A)=\sum_{\omega \in A} \mathbb{P}^B(\{\omega\})=\frac{\sum_{\omega \in A} \mathbb{P}(\{\omega\})}{\mathbb{P}(B)}=\frac{\mathbb{P}(A)}{\mathbb{P}(B)}
$$
If $A\subset\Omega$ but $A\nsubseteq B$  , we have $A\cap B\subset B$ . So
$$
\mathbb{P}^B(A)=\frac{\mathbb{P}(A \cap B)}{\mathbb{P}(B)}
$$
Usually we denote $\mathbb{P}^B(A)$  as $\mathbb{P}(A\mid B)$ , and call it conditional probability.

# 4. Random Variable

The **random variable(RV)** is neither random nor a variable. A random variable is a function $X:\Omega\rightarrow\mathbb{R}$ . (We assume the codomain as real number for simplicity, but it can be any measurable set)

For random variable $X$, when we write “$X=k$”, it means the set  $\{\omega\in\Omega:X(\omega)=k\}$ 

In this way, the notation $\mathbb{P}(X=k)$ means mapping the “$X=k$” set to real number from 0 to 1

## 4.1 Independent and uncorrelated

$X$ and $Y$ are **independent** RVs:
$$
P(X Y)=P(X) P(Y)
$$

Intuitively, independence means that knowing the value of one random variable gives no information about the other. Their behaviors are entirely unlinked.

For multiple RVs, $X_1\dots X_n$ . We say that they are **pairwise independent** if every pair $X_i$ and $X_j$ are independent for all i≠j. Pairwise independence is a relatively weak form of independence.

These RVs, $X_1\dots X_n$  are said to be **(fully) independent** if, for every subset $I\in[n]$ , we have
$$
\mathbb{P}\left[\bigcap_{i \in I} X_i\right]=\prod_{i \in I} \mathbb{P}\left[X_i\right]
$$
Note: Independence is expensive. For 𝚗 (different) nontrivial and independent events(RVs), the size of sample space $\mid\Omega\mid\geq2^n$ 

Two random variables $X$ and $Y$ are **uncorrelated** if their covariance is zero:
$$
\begin{gathered}
\operatorname{Cov}(X, Y)=\mathbb{E}[(X-\mathbb{E}[X])(Y-\mathbb{E}[Y])]=\mathbb{E}[X, Y]-\mathbb{E}[X] \mathbb{E}[Y]=0 \\
\mathbb{E}[X Y]=\mathbb{E}[X] \mathbb{E}[Y]
\end{gathered}
$$

Intuitively, uncorrelated random variables have no linear relationship between them.

Independence guarantees that $X$ and $Y$ are uncorrelated. But uncorrelated does not necessarily imply independence. RVs can be uncorrelated but non-linear dependent.

## 4.2 Geometric explanation

Random variables are functions defined on the sample space 𝝮, they satisfy the axioms of a vector space. So the set of RVs forms a vector space ( Hilbert space 𝗟²(𝝮) , technically)

For simplicity and WLOG, we ‘shift’ RVs by $X^\prime=X-\mathbb{E}[X]$ , $Y^\prime=Y-\mathbb{E}[Y]$ . Shift doesn’t affect properties of vectors. In this case, $\mathbb{E}(X)=\mathbb{E}(Y)=0$ 

The expectation corresponds to inner product in $L^2$
$$
\langle X, Y\rangle=\mathbb{E}[X Y]
$$

The $L^2$-norm of $X$ is
$$
\|X\|=\sqrt{\mathbb{E}\left[X^2\right]}
$$

The variance of $X$ is its squared 𝗟²-norm:
$$
\operatorname{Var}(X)=\mathbb{E}\left[(X-\mathbb{E}[X])^2\right]=\mathbb{E}\left[\left(X^{\prime}\right)^2\right]=\left\|X^{\prime}\right\|^2
$$

