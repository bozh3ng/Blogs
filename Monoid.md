We introduce 3 ways to define/understand the monoid.
## Set 
A monoid is a set with a binary operation $\langle S,\cdot \rangle$ which satisfies  
- Associativity: $(a \cdot b) \cdot c=a \cdot(b \cdot c)$  
- Identity element: $a\cdot e=e\cdot a=a$  
Roughly, it's a 'group-like' structure without an inverse. 

## One-object category  
A monoid is a one-object category. Morphisms in this category correspond to elements in a monoid.  Composition in this category corresponds to a binary operation in a monoid
```tikz
\usepackage{tikz-cd}
\begin{document}
\begin{tikzcd}
	\bullet
	\arrow[from=1-1, to=1-1, loop, in=55, out=125, distance=10mm]
	\arrow["e", from=1-1, to=1-1, loop, in=100, out=170, distance=10mm]
	\arrow[from=1-1, to=1-1, loop, in=280, out=350, distance=10mm]
\end{tikzcd}
\end{document}
```
![[./image/potential_assignment/20250716201114.png]]
(A group is a one-object groupoid)

## Commutative diagram 
We try to describe the behaviour of monoid using commutative diagram 
Choose an object $M \in$ Set, and morphisms $\mu: M \times M \rightarrow M$ , $\eta: 1 \rightarrow M$
- Associativity
$$\mu(\mu(a, b), c)=\mu(a, \mu(b, c)) \quad(\forall a, b, c \in M)$$
Commutative diagram:
```tikz
\usepackage{tikz-cd}
\begin{document}
\begin{tikzcd}
	{M\times M\times M} && {M\times M} \\
	{M\times M} && M
	\arrow["{\mathbf{1}_M\times \mu}", from=1-1, to=1-3]
	\arrow["{\mu\times\mathbf{1}_M}"', from=1-1, to=2-1]
	\arrow["\mu", from=1-3, to=2-3]
	\arrow["\mu"', from=2-1, to=2-3]
\end{tikzcd}
\end{document}
```
![[./image/potential_assignment/20250716201322.png]]
Note: $M \times M \times M \xrightarrow{1_M \times \mu} M \times M$ and $M \times M \times M \xrightarrow{\mu \times 1_M} M \times M$ are not automatically equal, they need to commute with $M \times M \xrightarrow{\mu} M$

- Identity element
$\mathbf{1}$ is the terminal object: 
$$!_M: M \rightarrow \mathbf{1}$$
In Set, it is singleton set $\{*\}$.  
We define $e:=\eta(*) \in M$. In this case, the morphism $\eta: 1 \rightarrow M$ needs to exist and be chosen (At least one such morphism on Set, but in general $\mathbf{1}\rightarrow X$ does not necessarily exist, e.g., Posets).  
To make $e$ behave like an identity:

$$\mu(e, a)=\mu(a, e)=a \quad(\forall a \in M)$$
Commutative diagram:
```tikz
\usepackage{tikz-cd}
\begin{document}
\begin{tikzcd}
	{\mathbf{1}\times M\cong M} && {M\times M} && {M\cong M\times\mathbf{1}} \\
	&& M
	\arrow["{\eta\times\mathbf{1}_M}", from=1-1, to=1-3]
	\arrow["{\mathbf{1}_M}"', from=1-1, to=2-3]
	\arrow["\mu", from=1-3, to=2-3]
	\arrow["{\mathbf{1}_M\times\eta}"', from=1-5, to=1-3]
	\arrow["{\mathbf{1}_M}", from=1-5, to=2-3]
\end{tikzcd}
\end{document}
```
![[./image/potential_assignment/20250716201406.png]]
Similarly, without this commutative diagram, $\mathbf{1} \times M \cong M \xrightarrow{\eta \times \mathbf{1}_M} M \times M$ and $M \times \mathbf{1} \cong M \xrightarrow{\mathbf{1}_M\times\eta} M \times M$ are not automatically equal.
