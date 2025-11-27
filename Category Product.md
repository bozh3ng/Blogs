**Definition**: Let $\mathcal{C}$ be a category and let $A,B$ be objects in $\mathcal{C}$ . A product of $A$ and $B$ is a triple $(P, \pi_1, \pi_2)$ where 
- $P$ is an object in $\mathcal{C}$, often denoted $A\times B$
- $\pi_1:P \rightarrow A$ and $\pi_2:P \rightarrow B$ are two morphisms (called projections) in $\mathcal{C}$
such that the following universal property holds:
For all objects $X$ in $\mathcal{C}$ and for all pairs of morphisms $f:X\rightarrow A$ and $g:X\rightarrow B$ , there exists a unique morphism $h: X \rightarrow P$ such that the diagram
![[file-20251101200333551.png]]
commutes

This definition is more informative than it looks. I will try to explain it based on my own understanding (I am pretty sure there is a better one). 

Remark:  
1. Product does not in general exist.  
2. Product is a triple $(A\times B, \pi_1, \pi_2)$ , not just $A\times B$, although usually we just use $A\times B$ for convince. 

The idea is we want to connect two objects $A$ and $B$, the compound is another object $A\times B$ (we assume the category is closed under product). We want $A\times B$  to be well-defined, which means given $A$ and $B$, there should be only one $A\times B$ (up to isomorphism).  
How do we characterize $A$ and $B$? By Yoneda, an object is all the morphisms that point in (out) of it.  So, for all objects $X$ and all morphisms $f:X\rightarrow A$, $g:X\rightarrow B$, we categorically mean select two objects $A$ and $B$ by their in-arrows. A unique morphism $h: X \rightarrow P$ means no matter how we 'probe' $A$ and $B$, the $P$ is unique (if it exists).  
Now we connect $A$ and $B$ uniquely, which is $P$, but what is the direction of the arrow between $A$ (or $B$ ) and $P$? One can argue that the direction $\pi_1:P \rightarrow A$ is given by definition, but this is not the only feasible definition. By duality, there exists a co-product with reversed arrows. In this case, we characterize $A$ and $B$ using their out-arrows, $\pi_1^{-1}:P \leftarrow A$  also needs to be reversed. Why does the projection direction depend on how we characterize objects? In other words, why this diagram 

![[file-20251101203753170.png]]
is not a correct definition? 
Argument 1: Assuming that $P$ makes this diagram commute, then $P$ is the product we want. If we set $P$ as the initial object, this diagram always commutes. But this is invalid, for example, in set, the product of two non-empty sets can not be empty.  
Argument 2: $\pi_1$ and $f$ are not in general unique. In this case
![[file-20251101204803846.png]]
By composition axiom, morphism $P\rightarrow X$ must not unique. So this definition is invalid. 


