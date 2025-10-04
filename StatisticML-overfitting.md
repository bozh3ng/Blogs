(why overfitting happens and why it is not too bad)
# 1. Intro
For simplify, we use $n$ samples with 2 features for binary classification
Feature space: $\left\{\left(x_i, y_i\right)\right\}_{i=1}^n$ drawn iid from $D$ on $\mathcal{X} \times \mathcal{Y}$. The distribution $D$ is unknown and will never be known. 
Label space: $\mathcal{Y}=\{-1,1\}$

Our goal is to find a function  $f: \mathcal{X} \rightarrow \mathcal{Y}$ that predicts $y$ from $x$
Define the true risk (loss) as
$$R^{\text {true }}(f):=\mathbb{P}_{(X, Y) \sim D}(f(X) \neq Y)=\mathbb{E}_{(X, Y) \sim D}\left[\mathbf{1}_{f(X) \neq Y}\right]$$
We have a distribution $D$, we keep sampling from it, then we try to find the distribution. If noise exist, then we can never perfectly separate data. Means $R^{\text {true }}(f)$ always greater than 0.   

Regression Function: 
$$\eta(x)=\mathbb{E}_{(X, Y) \sim D}(Y \mid X=x)$$
is the conditional expectation of the label given the feature vector. Because $Y=1$ or $Y=-1$, if $\eta(x)>0$, we guess label as 1, if $\eta(x)<0$, we guess label as -1 

Then we can define a (Bayes) classifier: 
$$t(x)=\operatorname{sign} \eta(x)$$
The true risk for Bayes classifier:
$$R^{\text {true }}(t)=\inf _f R^{\text {true }}(f)=R^*$$
is the best true risk we can actually get, is therefore the irreducible error built into the problem, a property of $D$. 
$R^*=0$ only when data is perfectly separable

Back to reality: 
$$R^{\text {emp }}(f)=\frac{1}{n} \sum_{i=1}^n \mathbf{1}_{\left[f\left(x_i\right) \neq y_i\right]}$$
is the training-set error we can measure on $f$ 

$f_n$ is the best rule we can obtain from finite data + regularisation, best function in practice.
$$f_n \in \operatorname{argmin}_{f \in \mathcal{F}} R^{\operatorname{emp}}(f)+C\|f\|^2$$
where $\mathcal{F}$ is function class , $C\|f\|^2$ works as regularization (penalty) term to keep $f$ simple 

$f^*$ is the best in (theory) class(unique)
$$R^{\text {true }}\left(f^*\right)=\inf _{f \in \mathcal{F}} R^{\text {true }}(f)$$

Summary: 
$R^{\text {true }}(f)=\mathbb{P}_{(X, Y) \sim D}(f(X) \neq Y)$: The true risk of a model $f$. 
$R^{\mathrm{emp}}(f)=\frac{1}{n} \sum_{i=1}^n \mathbf{1}_{\left[f\left(x_i\right) \neq y_i\right]}$: Empirical risk (training error) of $f$.
$R^*=\inf _f R^{\text {true }}(f)$: the lowest possible true risk over all measurable classifiers.
$f_n$ : the best learned model from $n$ samples. 
$f^* \in \arg \min _{f \in \mathcal{F}} R^{\text {true }}(f)$: the best model inside our hypothesis space $\mathcal{F}$.
$R^{\text {true }}\left(f_n\right)$: best error in practice, $f_n$ will be tested on new, unseen data generated from $D$, it's always greater than 0
$R^{\text {true }}\left(f^*\right)$: Best error inside our hypothesis class $\mathcal{F}$ . $R^{\text {true }}\left(f^*\right)=R^*$ if the hypothesis class rich enough
$R^{\text {emp}}\left(f_n\right)$: model performance in train dataset. A very complex model can drive it to 0. So it is meaningless.

Test error of (best in practice) - Test error of (best in theory) = 
$$R^{\text {true }}\left(f_n\right)-R^*=\left[R^{\text {true }}\left(f^*\right)-R^*\right]+\left[R^{\text {true }}\left(f_n\right)-R^{\text {true }}\left(f^*\right)\right]$$
= Approximation Error + Estimation Error 
$[R^{\text {true }}\left(f^*\right)-R^*]$ tells us whether our hypothesis class is **expressive** enough
$\left[R^{\text {true }}\left(f_n\right)-R^{\text {true }}\left(f^*\right)\right]$ tells us (1) how the finite sample deviates from the true distribution (**noise**) (2) **Algorithm** choice (penalty, early stopping, stochastic optimizer, etc. keep variance small but push we slightly away from $f^*$)

Note: We can't know anything about Approximation Error from looking at data 

# 2. Boundary
Let's try to bound $R^{\text {true }}\left(f_n\right)$.  (the best error inside our hypothesis class)
(basic idea: turn the invisible population risk into a controllable combination of visible training error plus a capacity-dependent penalty)

We can't measure $R^{\text {true }}$ because we don't have the whole distribution of data . $R^{\text {emp }}\left(f_n\right)$ is measurable. We rewrite the formula as
$$R^{\text {true }}\left(f_n\right)=R^{\text {emp }}\left(f_n\right)+\left[R^{\text {true }}\left(f_n\right)-R^{\text {emp }}\left(f_n\right)\right]$$
and try to give a boundary of $\left[R^{\text {true }}\left(f_n\right)-R^{\text {emp }}\left(f_n\right)\right]$ 

For each $f$ in $\mathcal{F}$ create a (0-1) **loss function** $g$ :
$$g(x, y)=\mathbf{1}_{f(x) \neq y}$$
$g$ is 1 if $f$ makes a mistake on $(x, y)$
($g$ is a measurable function $g: \mathcal{X} \times \mathcal{Y} \rightarrow \mathbb{R}$)
($f$ is a classifier $f: \mathcal{X} \rightarrow \mathcal{Y}$)
The collection of loss function:
$$\mathcal{G}=\left\{g:(x, y) \rightarrow \mathbf{1}_{f(x) \neq y}: f \in \mathcal{F}\right\}$$
There is a bijection between $\mathcal{F}$ and $\mathcal{G}$

Define a probability measure $P$ on $g$ :
$$P (g):=\int_{\mathcal{X} \times \mathcal{Y}} g(x, y) d P(x, y)$$
Relation between $R$ and $P$ :
$$R^{\text {true }}(f)=P^{\text {true }}(g)$$
$$R^{\mathrm{emp}}(f)=P^{\mathrm{emp}} (g)$$

Apply the probability operator, the true risk: 
$$P^{\text {true }} (g)=\mathbb{E}_{(X, Y) \sim D}\left[g(X, Y)\right]=\mathbb{P}(f(X) \neq Y)=R^{\text {true }}(f)$$

Empirical risk: 
$$P^{\mathrm{emp}} (g)=\frac{1}{n} \sum_{i=1}^n g\left(X_i, Y_i\right)$$

Since $g$ is the loss version of $f$ . $\left[R^{\text {true }}\left(f_n\right)-R^{\text {emp }}\left(f_n\right)\right]$ is equivalent to$[P^{\text {true }} (g_n)-P^{\mathrm{emp}} (g_n)]$


Define the notation of $n$ samples from $D$ as $\mathbf{Z} \sim D$ where 
$$Z_i=\left(X_i, Y_i\right)$$
So
$$P^{\text {true }} g-P^{\mathrm{emp}} g=\mathbb{E}_{\mathbf{Z} \sim D}[g(Z)]-\frac{1}{n} \sum_{i=1}^n g\left(Z_i\right)$$
As ${n} \rightarrow \infty$, the above approaches 0 .
But we don't have infinite data , we need to a lower bound for our real data 

Theorem (Hoeffding's Inequality). Let $Z_1 \ldots Z_n$ be $n$ iid random variables, and $h$ is a bounded function, $h(Z) \in[a, b]$. Then for all $\epsilon>0$ we have:
$$\mathbb{P}_{\mathbf{Z} \sim D}\left[\left|\frac{1}{n} \sum_{i=1}^n h\left(Z_i\right)-\mathbb{E}_{\mathbf{Z} \sim D}[h(Z)]\right|>\epsilon\right] \leq 2 \exp \left(-\frac{2 n \epsilon}{(b-a)^2}\right)$$
In our model $a=0$ and $b=1$. 
LHS means the probability that bad things happen , and it's less than some exponential formula 

We can bound how far the average if from expectation 
Make 
$$\delta=2 \exp \left(-\frac{2 n \epsilon^2}{(b-a)^2}\right)$$
So
$$\epsilon=(b-a) \sqrt{\frac{\log \frac{2}{\delta}}{2 n}}$$
Plug back to Hoeffding's, 
$$\mathbb{P}_{\mathbf{Z} \sim D}\left[\left|P^{\mathrm{emp}} g-P^{\mathrm{true}} g\right|>(b-a) \sqrt{\frac{\log \frac{2}{\delta}}{2 n}}\right] \leq \delta$$
This is the bound between true and empirical risk 

1-side Hoeffding's: 
$$\mathbb{P}_{\mathbf{Z} \sim D^n}\left[\mathbb{E}_{\mathbf{Z} \sim D^n}[h(Z)]-\frac{1}{n} \sum_{i=1}^n h\left(Z_i\right)>\epsilon\right] \leq \exp \left(-\frac{2 n \epsilon^2}{(b-a)^2}\right)=\delta$$
is the probability that the true risk is higher than the empirical risk 

Inversion trick: 
with probability at least $1-\delta$,
$$\mathbb{E}_{\mathbf{Z} \sim D}[h(Z)]-\frac{1}{n} \sum_{i=1}^n h\left(Z_i\right) \leq(b-a) \sqrt{\frac{\log \frac{1}{\delta}}{2 n}}$$
So
$$P^{\text {true }} g-P^{\mathrm{emp}} g \leq(b-a) \sqrt{\frac{\log \frac{1}{\delta}}{2 n}}$$
with probability at least $1-\delta$
Then
$$P^{\text {true }} g \leq P^{\mathrm{emp}} g+(b-a) \sqrt{\frac{\log \frac{1}{\delta}}{2 n}}$$
This is what we want, we want the true risk $P^{\text {true }} g$ to be small, but we can't measure it . We can measure empirical risk $P^{\mathrm{emp}} g$. 
Conclusion: If the data size $n$ is large, the $(b-a) \sqrt{\frac{\log \frac{1}{\delta}}{2 n}}$ part will be small 

# 3. Why the boundary doesn't work?
$$R^{\text {true }}(f) \leq R^{\mathrm{emp}}(f)+\sqrt{\frac{\log \frac{1}{\delta}}{2 n}}$$
It assumes that the function $f$ is a known quantity, which means if we choose a $f$ , what is the boundary of true risk of $R^{\text {true }}(f)$? In this case, the randomness is only in the data. 
(there exists a function $f$ which is good) 

What actually happens in learning
We first draw the data $\mathbf{Z}=\left\{\left(X_i, Y_i\right)\right\}_{i=1}^n$.
After seeing the data we choose
$$
f_n=\arg \min _{f \in \mathcal{F}}\left\{R^{\mathrm{emp}}(f)+C\|f\|^2\right\}
$$
Now $f_n$ is a data-dependent random variable.
The event
$$
P^{\text {true }} g_{f_n}-P^{\text {emp }} g_{f_n} \leq \epsilon
$$
must therefore hold simultaneously for whatever function the training algorithm ends up picking, this is a much stronger requirement.

## Overfitting
Recall symbols:
$R^{\mathrm{emp}}(f)=\frac{1}{n} \sum_{i=1}^n \mathbf{1}_{\left[f\left(x_i\right) \neq y_i\right]}$ : training (empirical) error
$R^{\text {true }}(f)=\mathbb{P}_{(X, Y) \sim D}[f(X) \neq Y]$ : test error 
$f_n$ : the data-dependent model we output, e.g. $f_n \in \arg \min _{f \in \mathcal{F}}\left\{R^{\operatorname{emp}}(f)+C\|f\|^2\right\}$
$\mathcal{F}$ : the whole hypothesis class you consider
$\mathcal{G}=\left\{\mathbf{1}_{[f(x) \neq y]}: f \in \mathcal{F}\right\}$ : the matching class of 0-1 loss functions

What Hoeffding tells us? 
If we pick one $f$ before looking at the data,
$$
\mathbb{P}\left[R^{\text {true }}(f)-R^{\text {emp }}(f)>\epsilon\right] \leq e^{-2 n \epsilon^2}
$$
This gives a boundary
$$
R^{\text {true }}(f) \leq R^{\text {emp }}(f)+\sqrt{\frac{\ln (1 / \delta)}{2 n}}
$$

But the truth is we are searching for $f$
First we see the sample $\mathbf{Z}=\left\{\left(x_i, y_i\right)\right\}_{i=1}^n$
Then we choose
$$
f_n=\arg \min _{f \in \mathcal{F}} R^{\mathrm{emp}}(f)
$$
depends on (training) data 

If $\mathcal{F}$ is large, we can find a $f_n$ which makes $R^{\mathrm{emp}}\approx 0$ 
But in this case, even if with small noise, $f_n$ carves out these points in a high dimensional space, making a over-fit area, which magnify the error in test data. The true error $R^{\text {true }}\left(f_n\right)\gg 0$. This is **overfitting**
Usually $\mathcal{F}$ is large, because for a class with VC dimension $d$ we need $n \gg d$ to make the uniform bound small.

### Statistically analyze
$\mathbf{Z}$: the whole training sample $\left\{\left(X_i, Y_i\right)\right\}_{i=1}^n$
$S_g$: "good-set" for a fixed loss function $g$ 
$g_n$ : the loss function that corresponds to the classifier $f_n$ chosen after seeing $\mathbf{Z}$
$S_{g_n}$: good-set for that particular $g_n$ 

For every fixed, non-random loss function $g \in \mathcal{G}$ has its "good set" of samples
$$
S_g=\left\{\mathbf{Z}: P^{\text {true }} g-P^{\text {emp }} g \leq \epsilon\right\}
$$
Hoeffding tells us 
$$\mathbb{P}\left[\mathbf{Z} \in S_g\right] \geq 1-\delta\quad\text{or}\quad\mathbb{P}\left[\mathbf{Z} \notin S_g\right] \leq \delta$$
means if we were forced to use that same $g$ no matter what data arrive, the chance of a bad generalisation gap is at most $\delta$.

For a finite class $|\mathcal{G}|=N$, probability that some $g \in \mathcal{G}$ is bad is
$$
\mathbb{P}\left[\exists g \in \mathcal{G}: \mathbf{Z} \notin S_g\right] \leq N \delta .
$$
 In practice we look at the data first and then select $g_n \in \mathcal{G}$. The event
$$
\left\{\mathbf{Z} \notin S_{g_n}\right\}
$$
implies that at least one $g$ (namely the chosen one) violates the Hoeffding bound.
Therefore
$$
\mathbb{P}\left[\mathbf{Z} \notin S_{g_n}\right] \leq \mathbb{P}\left[\exists g: \mathbf{Z} \notin S_g\right] \leq N \delta .
$$

The probability of overfitting is $N \delta$, means if we pick any hypothesis from a hypothesis class, the probability of overfitting is not bounded by $\delta$. 

To bound the probability of over-fitting, we need a uniform bound for all hypothesis. 

# 4. The Uniform Bound
Uniform deviations
$$R^{\text {true }}\left(f_n\right)-R^{\text {emp }}\left(f_n\right) \leq \sup _{f \in \mathcal{F}}\left(R^{\text {true }}(f)-R^{\text {emp }}(f)\right)$$
$\mathcal{F}$ (or equivalently $\mathcal{G}$ ) is finite

Idea: One hypothesis is Hoeffding, we collect many hypotheses and take a union 

Let the hypothesis class be finite
$$
\mathcal{F}=\left\{f_1, \ldots, f_N\right\}
$$
For each $f_k$ set the per-function confidence level
$$
\delta_k=\delta / N
$$
Apply Hoeffding to each $f_k$: 
$$
\mathbb{P}\left[\exists f \in \mathcal{F}: R^{\text {true }}(f)-R^{\text {emp }}(f)>\sqrt{\frac{\ln N+\ln (1 / \delta)}{2 n}}\right] \leq \sum_{k=1}^N \delta_k=\delta .
$$

Theorem. (Ockham's Razor) With probability $\geq 1-\delta$, every hypothesis in $\mathcal{F}$ satisfies
$$
R^{\mathrm{true}}(f) \leq R^{\mathrm{emp}}(f)+\sqrt{\frac{\ln N+\ln (1 / \delta)}{2 n}}
$$

Prefer the simple hypothesis class ($N$ ) and more data ($n$).

This theorem tells us that, if the function class is finite, $|\mathcal{F}|=N$, with high probability
$$
\sup _{f \in \mathcal{F}}\left[R^{\text {true }}(f)-R^{\mathrm{emp}}(f)\right] \approx \sqrt{\log N / n}
$$



# VC dimension



