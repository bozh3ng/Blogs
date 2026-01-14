---
~
---
# 1. Confusion

**Statement**: Toss a coin, the probability of getting a head is 0.5.

There are (at least) two common explanations for this statement: Frequentist and Bayesian.

In the Frequentist interpretation, probability is defined as the long-run tests and observations. So, if we believe the statement, and we toss the coin 100 times, we will get about 50 heads, maybe 53 maybe 45, but around 50. If we toss the coin many many times , let’s say A times, we will observe exactly A/2 heads.  
While Bayesian said, "We don’t know the probability at the beginning; we guess one (as a prior)." Let’s (tentatively) believe the probability of getting a head is 1; it doesn’t matter whether the belief is right or wrong. Then we update it with more tests. We toss it again, we observe a tail, then the probability can not be 1, we update our belief (as posterior). We toss it again, we update, we toss again… If we toss and update many many times, the belief (as the result of Bayes’ theorem) is 0.5

They both intuitively make sense, but again, what does it mean if something happens with probability? If I were told I have a 0.4 probability of passing an exam and can attend it only once, then either I pass it or I don’t. What does it mean that I can pass it with probability 0.4? There is no such thing as 0.4 of a diploma. I will take the exam anyway, and I either pass or fail, what is the difference to me between 0.9 and 0.1 probability of passing?


# 2. (Discrete) Probability
  
**Definition**: A finite probability space ($\Omega$ , $\mathbb{P}$) is a finite set $\Omega$  and its (probability) measure ℙ which satisfies  
- $\mathbb{P}(\Omega)=1$  
- $\forall A\in \Omega,\mathbb{P}\geq0$

Technically speaking, a probability space is a triple $(\Omega,\mathcal{A}, \mathbb{P})$; we omit the sigma-algebra to avoid more confusions.

Loosely speaking, probability is a function that can map an element in a set to a real number between 0 and 1.

Toss a coin, the probability of getting a head is 0.5, which means: We construct a set with all the cases of tossing a coin. One case is that we get a head. The probability we are discussing is a function that maps the event “head case” to the real number 0.5.  
I can pass an exam with probability 0.4; that is, there exists a function that maps the event “I pass the exam” to the real number 0.4. It is no different from mapping the event to 0.9 or mapping the event to 0.1. Mathematics is not always useful in the real world.
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

Independence guarantees that $X$ and $Y$ are uncorrelated. But uncorrelated does not necessarily imply independence. RVs can be uncorrelated but non-linearly dependent.

## 4.2 Geometric explanation

Random variables are functions defined on the sample space 𝝮, they satisfy the axioms of a vector space. So the set of RVs forms a vector space ( Hilbert space 𝗟²(𝝮) , technically)

For simplicity and WLOG, we ‘shift’ RVs by $X^\prime=X-\mathbb{E}[X]$ , $Y^\prime=Y-\mathbb{E}[Y]$ . Shift doesn’t affect the properties of vectors. In this case, $\mathbb{E}(X)=\mathbb{E}(Y)=0$ 

The expectation corresponds to the inner product in $L^2$
$$
\langle X, Y\rangle=\mathbb{E}[X Y]
$$

The $L^2$-norm of $X$ is
$$
\|X\|=\sqrt{\mathbb{E}\left[X^2\right]}
$$

The variance of $X$ is its squared $L^2$-norm:
$$
\operatorname{Var}(X)=\mathbb{E}\left[(X-\mathbb{E}[X])^2\right]=\mathbb{E}\left[\left(X^{\prime}\right)^2\right]=\left\|X^{\prime}\right\|^2
$$

# 5. Expectation
First recall **probability space** is a triple $(\Omega, \mathcal{F}, P)$ , where $\mathcal{F}$ is a sigma-algebra, the **probability** $P$ is a function $P:\mathcal{F}\rightarrow[0,1]$ that satisfies non-negativity, normalization, countable additivity. 

For a continuous random variable $X$ , the **Probability Density Function** (PDF) $f(x)$ is a function such that:
$$
P(a \leq X \leq b)=\int_a^b f(x) d x
$$
Or
$$
P(A)=\int_A f(x) d x \quad \text { for all sets } A
$$
Note that $f(x)$ is not $P(X=x)$. Rather, $f(x)dx$ represents the infinitesimal probability that X falls in a tiny interval around $x$.

For any measurable function $g$, the **expectation** of function $g$ in probability $P$ is defined as 
$$
\mathbb{E}[g(X)]:=\int g(x) d P(x)
$$

There is a bit confusing notation: $P(x)$ is not a function of single point $x$, $P(\cdot)$ is a measure acts on sets, not points: 
- $P(\{x\})$ is the probability of the singleton set $\{x\}$
- $P([a,b])$ is probability that X falls in $[a,b]$
- $P(A)$ is the probability of event A
So in $P(x)$, the $x$ is a notation of sets, $P$ is a measure that assigns probabilities to sets.

Another a bit confusing notation: What does $dP(x)$ mean?
$dP(x)$ is a notation Lebesgue integration, means an infinitesimal "probability element." We can analogy it to the common $dx$ in Riemann integral which represents an infinitesimal "length element." 
So in $dP(x)$, the $x$ is not the input parameter for $P$, it indicates the variable of integration.
A more honest notation is:
$$
\int g d P\quad \text { or }\quad \int g(x) P(d x)
$$
In $\int g(x) P(d x)$, the $x$ in $P(dx)$ represents a single point in the sample space (e.g., a real number in $\mathbb{R}$).

Back to 
$$
\mathbb{E}[g(X)]:=\int g(x) d P(x)
$$
If $P$ has density $f$, which means there exists a $f$ such that 
$$
P(A)=\int_A f(x) d x \quad \text { for all sets } A
$$
Then: 
$$\int g(x) d P(x)=\int g(x) f(x) d x$$
Note: In $\int g(x) d P(x)$, the first $x$ in $g(x)$ means a single point, but the second $x$ in $P(x)$ means a set, because $P$ is a probability measure. In $\int g(x) f(x) d x$, all the $x$ means a single point.

## Expectation IS Integration
The connection emerges: expectation is integration against a probability measure. If $X \sim P$ (meaning $X$ is distributed according to $P$ ), then by definition:
$$
\mathbb{E}_{X \sim P}[g(X)] {:=} \int g(x) d P(x)
$$
If $f$ is a density for probability measure $P$ , then for any measurable $g$ :
$$
\int g(x) f(x) d x=\int g(x) P(d x)=\mathbb{E}_{X \sim P}[g(X)]
$$
This is a common trick to study intractable integral using probability tools, especially Monte Carlo. (See [[PML brief note-1]] ELBO)

Nice! Then how do we know $f$ is a density? 
A function $\mathrm{f}: \mathbb{R} \rightarrow \mathbb{R}$ is a valid probability density if and only if:
1. Non-negativity:
$$
f(x) \geq 0 \quad \text { for all } x
$$
2. Normalization:
$$
\int_{-\infty}^{\infty} f(x) d x=1
$$
3. Measurability: this condition almost always satisfied.

A small caveat: All the statements need $g(x)$ to be bounded or well-behaved so $\mathbb{E}[|g(X)|]<\infty$. 

Another small caveat: Density and probability are not one-to-one correspondence: Discrete distributions have no density; when a density exists, it's unique to probability only "almost everywhere."

## What is distribution? 
Roughly it means probability of random variable $X$. The distribution of a random variable ${X}$ is the probability measure $P_X$ on the target space defined by:
$$
P_X(A)=P(X \in A)
$$
It tells us how probability is "distributed" across possible values of $X$ .
