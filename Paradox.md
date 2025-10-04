# [Birthday Paradox](https://en.wikipedia.org/wiki/Birthday_problem#:~:text=In%20probability%20theory%2C%20the%20birthday,that%20probability%20to%20exceed%2050%25)
## Question
If we have a set of $n$ randomly chosen people, what is the probability that at least two will share the same birthday? the counterintuitive fact is that only 23 people are needed for that probability to exceed 50%.

## Solution
We assume that 1 year has 365 days and birthdays of different people are independent.
Probability that all birthdays are different: 
$$P_{unique}=\prod_{k=0}^{n-1} \frac{365-k}{365}$$
Probability at least one shared birthday
$$
P_{\text {shared }}(n)=1-P_{\text {unique }}(n) .
$$
When $n=23$, $P_{\text {shared }}(23) \approx 1-0.492702=0.507298$

## Why counterintuitive? 
Our intuition is usually **linear** : add one more person, add one more chance, while the real story is **combinatorial** : add one more person, add a whole bundle of new pairs that could match. And pairs grow much faster than people
With $n$ people there are
$$
\binom{n}{2}=\frac{n(n-1)}{2}
$$
possible pairs of birthdays.

When we invite the 23-rd guest, we've created $\binom{23}{2}-\binom{22}{2}=22$ new pairs at once. With 23 people, we have 253 pairs. 
For any particular pair the chance of a match is $1 / 365 \approx 0.27 \%$.
Intuitively (this is not the correct answer), we have $253 \times \frac{1}{365} \approx 0.69$ probability that these pairs collision. 


# [Monty Hall problem](https://en.wikipedia.org/wiki/Monty_Hall_problem)
Suppose you're on a game show, and you're given the choice of three doors: Behind one door is a car; behind the others, goats. You pick a door, say No. 1, and the host, who knows what's behind the doors, opens another door, say No. 3, which has a goat. He then says to you, "Do you want to pick door No. 2?" Is it to your advantage to switch your choice?

## Intuition 1
We know that $P(car)=\frac{1}{3}$，$P(goat)=\frac{2}{3}$.  What is the probability of win if we stay $P(\text{stay and win})$ ? 
If we are in situation $P(car)=\frac{1}{3}$, we stay, we win. 
If we are in situation $P(goat)=\frac{2}{3}$, we stay, we lose. 
So $P(\text{stay and win})=\frac{1}{3}$

## Intuition 2
Regardless of our initial choice (car or goat), the host can always reveal a goat behind another door. This action is trivial and provides no new information, so our win probability remains unchanged ($\frac{1}{2}$ or $\frac{1}{3}$). 

## Case 1
The host—who knows the contents—must open a different door with a goat and must offer the switch. (The host’s action is not random, it’s constrained by the rules)

Let's build a probability space 
Sample space :
$$
\Omega=\left\{(c, i, h) \in\{1,2,3\}^3: h \neq c, h \neq i, \text { and } h \text { obeys the host rule }\right\} .
$$
- $c$ - door that hides the car
- $i$ - contestant's initial choice
- $h$ - door the host opens

The host rule:
- If $c=i$ the host randomly picks one of the two remaining goats, so $h\in\{1,2,3\} \backslash\{c\}$ with probability $\frac{1}{2}$ each.
- If $c \neq i$ there is only one goat door available, the host must open it, $h\in\{1,2,3\} \backslash\{c,i\}$ with probability 1

That leaves 12 elements in $\Omega$

```
cih
112
113
123
132
213
221
223
231
312
321
331
332
```

We take sigma-algebra as $\mathcal{F}=\mathcal{P}(\Omega)$
For $(c, i, h) \in \Omega$
$$
P\{(c, i, h)\}= \begin{cases}\frac{1}{3} \cdot \frac{1}{3} \cdot \frac{1}{2}, & \text { if } c=i  \\ \frac{1}{3} \cdot \frac{1}{3} \cdot 1, & \text { if } c \neq i \end{cases}
$$
$(\Omega, \mathcal{F}, P)$ is a probability space.

Define random variables on $\Omega$
$$
C(c, i, h)=c, \quad I(c, i, h)=i, \quad H(c, i, h)=h .
$$

Notice our $\Omega$ is perfectly symmetric under relabelling. So WLOG, we can define observation(condition) 
$$E=\{I=1, H=3\} \in \mathcal{F}$$

Whether we win or not depends on $C$. Define events under condition $E$
- Stay-win: $T=\{C=I\mid E\}$
- Switch-win: $S=\{C \neq I\mid E\}$

Under condition $E$, $C$ can only be 1 or 2 
$$\begin{aligned} & P(C=1 \mid E)=\frac{P(C=1, I=1, H=3)}{P(E)}=\frac{\frac{1}{3} \frac{1}{3} \frac{1}{2}}{\frac{1}{3} \frac{1}{3} \frac{1}{2}+\frac{1}{3} \frac{1}{3}}=\frac{1}{3}, \\ & P(C=2 \mid E)=\frac{P(C=2, I=1, H=3)}{P(E)}=\frac{\frac{1}{3} \frac{1}{3}}{1 / 18+1 / 9}=\frac{2}{3} .\end{aligned}$$

So
$$
P(T)=\frac{1}{3}, \quad P(S)=\frac{2}{3} .
$$

## Case 2
Same as before 
$C \in\{1,2,3\}$, $P(C=c)=1 / 3$.
$I \in\{1,2,3\}$, $P(I=i)=1 / 3$.
Random host : Without looking, the host chooses uniformly at random one of the two doors $\{1,2,3\} \backslash\{I\}$. Call that door $H$. The door $H$ happens to be a goat. 

Now our sample space becomes 
$$\Omega=\left\{(c, i, h) \in\{1,2,3\}^3: h \neq i\right\}$$
We take sigma-algebra as $\mathcal{F}=\mathcal{P}(\Omega)$
For $(c, i, h) \in \Omega$
$$P\{(c, i, h)\}=\frac{1}{3} \cdot \frac{1}{3} \cdot \frac{1}{2}=\frac{1}{18}$$
$(\Omega, \mathcal{F}, P)$ is a probability space.
Now we have 18 elements in $\Omega$
```
cih
112
113
121  -- new
123
132
131  -- new
212  -- new
213
221
223
231
232  -- new
313  -- new 
312
321
323  -- new
331
332
```

In this sample space, host might open a goat door($c\neq h$), might open a car door($c=h$). 
In reality, the event "door $H$ is not the car" happened
$$G=\{(c, i, h): c \neq h\}$$
This event happens with probability 
$$P(G)=\frac{12}{18}=\frac{2}{3}$$
The subspace $\Omega_G$ under event $G$ is the same as space in case 1 . But the probability is different 
For every remaining triple $(c, i, h) \in G$,
$$P_G\{(c, i, h)\}=\frac{P\{(c, i, h)\}}{P(G)}=\frac{1 / 18}{2 / 3}=\frac{1}{12}$$
Reason: [[Probability-1]] Conditional Probability. Intuitively, since the host randomly chose a door, each option has an equal probability.

In subspace $\Omega_G$, we still define condition as 
$$E=\{I=1, H=3\} \in \mathcal{F}$$
And events 
- Stay-win: $T=\{C=I\mid E\}$
- Switch-win: $S=\{C \neq I\mid E\}$

$$P_G(E)=P_G(I=1, H=3)=1 / 6$$
So
$$\begin{aligned} & P(C=1 \mid E)=\frac{P(C=1, I=1, H=3)}{P(E)}=\frac{1/12}{1/6}=\frac{1}{2}, \\ & P(C=2 \mid E)=\frac{P(C=2, I=1, H=3)}{P(E)}=\frac{1/12}{1/6}=\frac{1}{2} .\end{aligned}$$

Hence 
$$
P(T)=\frac{1}{2}, \quad P(S)=\frac{1}{2} .
$$

## Intuition 3
The host’s move tells you more than "we have a door which is goat" , but "this door is a goat"
Because he chose that door under the rule "never show the car", his action implicitly says:  
"Either you already had the car (1 in 3 chance) or, if not, I have just pointed out the only goat door I was allowed to open (2 in 3 chance)."  
That filtered choice is the information-laden signal, and it is what makes switching the better bet.

## But...?
Imagine we're on a game show. We choose one door, and the host opens another to reveal a goat. We don't know if the host knows what's behind his chosen door. Should we switch our choice? How do these calculations helps us? 
Treat the uncertainty about the host as another random variable and use Bayes’ rule.
$K$: Informed host
$R$: Random host 
$G$: The event host opens a door which is a goat. 
Set $q=P(K)$
$$P(G \mid K)=1$$
$$P(G \mid R)=\frac{2}{3}$$
$$P(K \mid G)=\frac{P(G \mid K) q}{P(G \mid K) q+P(G \mid R)(1-q)}=\frac{q}{q+\frac{2}{3}(1-q)}$$

Set $p^*=P(K \mid G)$ 
$$\begin{gathered}P(\text { win by switching } \mid G)=p^* \cdot \frac{2}{3}+\left(1-p^*\right) \cdot \frac{1}{2}=\frac{1}{2}+\frac{p^*}{6}, \\ P(\text { win by staying } \mid G)=p^* \cdot \frac{1}{3}+\left(1-p^*\right) \cdot \frac{1}{2}=\frac{1}{2}-\frac{p^*}{6} .\end{gathered}$$

Switching is never worse



# [Russell's paradox](https://en.wikipedia.org/wiki/Russell%27s_paradox)
Or barber's paradox: The barber is the "one who shaves all those, and those only, who do not shave themselves". The question is, does the barber shave himself?
This is a self-reference paradox, which leads to inconsistency(something both right and wrong). 

## Recall: Naïve comprehension
(Naïve comprehension) For every logical property $P(x)$ there exists a set consisting of all things that satisfy $P$. 
Using set-builder notation:
$$\{x \mid P(x)\}$$
Using predicate logic:
$$\forall P(\exists A \forall x[x \in A \Longleftrightarrow P(x)])$$
No background set $A$ is needed

### Building Russell’s set
Take the particular property
$$
P(x): x \notin x .
$$
Applying the naïve comprehension with this $P$ we get a set $R$ such that
$$
\forall x(x \in R \Longleftrightarrow x \notin x) .
$$
Written in set-builder notation:
$$
R=\{x \mid x \notin x\}
$$
Is $R$ an element of itself?
- Assume $R \in R$. By the defining condition, $R \in R$ implies $R \notin R$. Contradiction.
- Assume $R \notin R$. Then $R$ satisfies the property " $x \notin x^{\prime \prime}$, so $R \in R$. Contradiction.
Inconsistency !
## Axiom schema of specification
Formally, for any set $A$ and its (not necessary proper) subset $B$, every first-order formula $P(x)$ with free variable $x$ :
$$
\forall A \exists B \forall x\left(x \in B \Longleftrightarrow x \in A \wedge P(x)\right) .
$$
(Because there is one axiom for every formula $P$, the principle is called an axiom schema rather than a single axiom.)

Compared with naïve comprehension, this axiom allows us to form a set with property $P(x)$, but only inside a pre-existing set $A$:
$$\{x \in A \mid P(x)\}$$
Claim: A universal set containing everything (which is used in naïve comprehension) cannot exist if we want to uphold the axiom schema of specification and avoid Russell's paradox.

### Why no universal set? 
Inside the deductive system, we can't just invent a symbol $A$ and say "let $A$ be the set of all sets". We must prove it exists or add it as an axiom. We can't prove the universal set exists using axioms, so we add it as an axiom. 

Formally, "let $A$ contain every set" means adding an axiom:
$$\exists A \forall x(x \in A)$$
Choose the property $P(x): x \notin x$.
Separation yields:
$$
R=\{x \in A \mid x \notin x\}
$$
Because $A$ is an universal set, the clause "$x \in A$" is automatically true for every $x$. This leads to Russell's set (inconsistent):
$$
R=\{x \mid x \notin x\}
$$
So, if we admit both Separation and consistency, then a universal set cannot exist.
(We can also use other axioms to prove a universal set cannot exist, for example axiom of power set + Cantor's theorem, axiom of regularity, etc.)

## How this helps to avoid Russell's paradox?
Axiom schema of specification -> No universal set -> Russell's set can not be constructed. 
The notation $R=\{x \mid x \notin x\}$ is not a set.

## (Optional)Axiom of regularity
### Recall: Infinite
To understand this, first we give a little introduction to infinite.
Take natural number for example. In element level, a single natural number $n$ itself always finite. In set level, the set to natural number $\mathbb{N}$ is infinite, whose cardinality is $\aleph_0$ 

Why $n$ is finite? 
No matter which $n$ we choose, we can finish counting up to $n$ in finitely many steps
Why $\mathbb{N}$ infinite? 
A set is called infinite when no fixed natural number can exhaust its elements.
Or, a set $X$ is infinite iff there exists a bijection between $X$ and a proper subset of $X$.
We can use:
$$
\begin{gathered}
f: \mathbb{N} \longrightarrow \mathbb{N} \\
n\mapsto n+1
\end{gathered}
$$
### Axiom of regularity
Formal statement
$$\forall A(A \neq \varnothing \Longrightarrow \exists x(x \in A \wedge x \cap A=\varnothing))$$
Every non-empty set $A$ has an element that shares no elements with $A$ itself.

Let's have an example 
Let
$$
A=\{\{1\},\{2,3\},\{4,5,6\}\}, \quad x=\{1\} \in A
$$
- Elements of $x$ : 1 .
- Elements of $A$ : $\{1\},\{2,3\},\{4,5,6\}$.
The number 1 is not itself one of those three sets, so
$$
x \cap A=\varnothing
$$

If we think of the membership relation $\in$ as a tree whose root is the set $A$, we follow one branch and go deeper and deeper, eventually we will arrive the bottom. 

The ordinal-rank viewpoint
Define the rank of a set by transfinite recursion:
$$
\operatorname{rk}(x)=\sup \{\operatorname{rk}(y)+1: y \in x\} .
$$
Each element $n \in \omega$ is the set $\{0,1, \ldots, n-1\}$. $\operatorname{rk}(n)=n$ is finite. 
But the set $\omega$ itself $\operatorname{rk}(\omega)=\sup \{\operatorname{rk}(n)+1: n \in \omega\}$ is infinite

We can analogy this to natural number: every individual natural number is finite, but the whole set $\mathbb{N}$ is infinite.

Finite per instance does not imply a finite global bound. Regularity guarantees that every downward $\in$-chain is finite; it does not say there is one finite number that caps them all.

Regularity is an existence axiom: it says there is such a bottom element; it does not give an algorithm for finding it.

This axiom constraints the behaviors of membership relation $\in$ 
- No membership loops. We can't have $x \in x$, or a cycle $x_0 \in x_1 \in \cdots \in x_k=x_0$.
- No infinite descending $\varepsilon$-chains. There is no sequence $x_0 \ni x_1 \ni x_2 \ni \cdots$ that goes on forever.

Consequence: $x \notin x$ for all sets $x$. (Apply the axiom to $A=\{x\}$, then we have $x \cap\{x\}=\varnothing$, so $x \notin x$.)

No set can contain itself.
If something contains itself, then it is not a set.
But every set is a subset of itself ( $x \subseteq x$ ).
There is something "larger" than the set.

### Note
Regularity by itself does not stop the paradox
If we already have a $R$ which satisfies
$$(\exists R) \forall x[x \in R \Longleftrightarrow x \notin x]$$
This $R$ gives a contradiction.
Regularity says
$$
\forall x(x \notin x) .
$$
but it cannot override the existence claim
In other words: Regularity does not prevent $R$ from being postulated; it only tells you $R \notin R$ after $R$ has already been postulated.


# [Banach-Tarski paradox](https://en.wikipedia.org/wiki/Banach%E2%80%93Tarski_paradox)
This paradox is related to Axiom of Choice (AC)
Note that this paradox does not hold in $\mathbb{R}^2$. This is because $\mathbb{R}^2$ has less symmetries compared to $\mathbb{R}^3$ 
#TODO 

## Axiom of Choice (AC)
Intuition: If we have an infinite family $\left\{X_i\right\}_{i \in I}$, ZF alone cannot guarantee even existence of an element of $\prod_{i \in I} X_i$. The construction may stall forever. AC gives a choice function $f(i) \in X_i$ for each $X_i$ that we can do simultaneously.
Roughly, AC let us commute from "finite" data to a total object that may live at a higher cardinality.

## Example usage of AC
### Not Lebesgue measurable set
There exist sets which are not Lebesgue measurable

### Product Topology 
Given an underlying set 
$$X=\prod_{i \in I} X_i$$
and a projection maps 
$$\pi_i: X \rightarrow X_i,\quad\left(x_j\right)_{j \in I} \mapsto x_i$$
The product topology is the smallest topology on $X$ that makes every projection $\pi_i$ continuous.

In ZF, the Cartesian product can be formed as a set of functions 
$$x: I \rightarrow \bigcup_i X_i$$
with $x(i) \in X_i$.

If $I$ is infinite, even if every $X_i$ is not empty, without AC, the Cartesian product not necessary to be non-empty 

We need AC to prove Tychonoff theorem 

### A small quiz 
Proof: Second countable is Lindelöf 
Recall 
Second countable: countable basis 
Lindelöf: any open cover has countable subcover 
Let $X$ be second countable, so there exists a basis 
$$\mathcal{B}=\bigcup_{i=1}^{\infty} B_i$$
Choose any cover $\mathcal{C}$ of $X$
$$\mathcal{C}=\bigcup_{I} C_j$$
$j$ might be uncountable
$C_j$ is open, so for $\forall C_j, \exists B_i$ such that 
$$B_i\subset C_j$$
(AC): Choose one $C_k$ from every $C_j$ such that 
$$B_i\subset C_k$$
Collect them as $\{C_k\}$ which is countable
Next we argue that $\{C_k\}$ is a subcover for any cover of $X$
For $\forall x\in X$, because basis, 
$$\exists B_i\in\mathcal{B}\quad s.t.\quad x\in B_i$$
Also 
$$B_i\subset C_k$$
So $\{C_k\}$ covers all $x$
We can choose any cover $\mathcal{C}=\bigcup C_j$
So $X$ is Lindelöf





