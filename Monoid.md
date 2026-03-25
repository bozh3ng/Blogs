A monoid is one of the simplest algebraic structures -- a set with an associative binary operation and an identity element. It admits at least three equivalent descriptions, each revealing different aspects.

## As a set with a binary operation
A monoid is a set with a binary operation $\langle S,\cdot \rangle$ which satisfies  
- Associativity: $(a \cdot b) \cdot c=a \cdot(b \cdot c)$  
- Identity element: $a\cdot e=e\cdot a=a$  
Roughly, it's a 'group-like' structure without an inverse. 

## As a one-object category
A monoid is a one-object category. Morphisms in this category correspond to elements of the monoid, and composition corresponds to the binary operation. The identity morphism corresponds to the identity element $e$, and the associativity of composition gives associativity of the binary operation.
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
(A group is a one-object groupoid -- adding inverses to every morphism turns the one-object category into a groupoid, equivalently turning the monoid into a group.)

## Via commutative diagrams
We describe the monoid axioms using commutative diagrams. A commutative diagram asserts that all directed paths with the same start and end yield the same composite morphism.
Choose an object $M \in \mathbf{Set}$, and morphisms $\mu: M \times M \rightarrow M$ , $\eta: 1 \rightarrow M$
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
Note: $M \times M \times M \xrightarrow{1_M \times \mu} M \times M$ and $M \times M \times M \xrightarrow{\mu \times 1_M} M \times M$ are not automatically equal. The two maps become equal only after composing with $\mu$; that equality is precisely associativity.

- Identity element
$\mathbf{1}$ is the terminal object: 
$$!_M: M \rightarrow \mathbf{1}$$
In Set, it is singleton set $\{*\}$.  
We define $e:=\eta(*) \in M$. Here $\eta$ is part of the monoid structure -- it is chosen data, not merely an existence claim. In $\mathbf{Set}$, morphisms $\mathbf{1} \to M$ always exist (any function from a singleton picks an element of $M$), but $\eta$ specifies _which_ element serves as the identity.

Remark: In a general monoidal category, a morphism from the unit object to a given object need not exist. For example, in certain monoidal categories the unit $I$ may have no morphism to some objects, so the existence of $\eta$ is a genuine requirement.
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

This diagrammatic definition is the one that generalizes: replacing $\times$ with a tensor product $\otimes$ gives a monoid object in any monoidal category, not just $\mathbf{Set}$.
