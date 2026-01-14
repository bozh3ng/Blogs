# The calculus perspective: dx and $\Delta x$ 
This is a direct and well-known perspective. $\Delta x$ is a finite change in x. $dx$ is an infinitesimal change in x. If we accept limit(infinite), the derivative definition:
$$
\frac{d f}{d x}=\lim _{\Delta x \rightarrow 0} \frac{f(x+\Delta x)-f(x)}{\Delta x}=\lim _{\Delta x \rightarrow 0} \frac{\Delta f}{\Delta x}
$$
So $df / dx$ is the limit of the ratio $\Delta f / \Delta x$. In a sense, "d" is the infinitesimal version of  "$\Delta$". So "dx" means "an infinitely small piece of x".

But next let me strenuously introduce a differential geometry perspective. Why? Because it is more fundamental, it reflects the cognitive model: what is the intrinsic truth we believe? How do we describe it? 

# The differential geometry perspective
The general idea: $dx$ is a function that can represent tangent vectors in x-coordinate. $dx(v)$ is a representation of $v$ in x-coordinate. 

First we define $x$ as a function: 
$$x:\Omega\rightarrow \mathbb{R}^n.$$

There are many ways to understand it. For example, if $x$ is smooth, the image of $x$ is a manifold. Here we view $x$ as a coordinate map. 

$x:\Omega\rightarrow \mathbb{R}^n$ is a coordinate map assigns to each point $p \in \Omega$ an n-tuple of real numbers:
$$
p \mapsto\left(x_1(p), x_2(p), \ldots, x_n(p)\right)
$$

We can think that $x$ describe $\Omega$ using $n$ real numbers, but these numbers are independent, so $x$ is a n-dimensional coordinate of $\Omega$. 

Then we define $v$ as a tangent vector at point $p\in\Omega$. 

Let's take our general idea a step further: $dx$ is a function whose input is $v$ and output is $n$ real numbers : $[dx_1(v),dx_2(v),dx_3(v)\cdots dx_n(v)]$. Each $dx_i(v)$ is a component of $dx(v)$. 

Recall that a vector contains both speed (scalar) and direction. Here $v$ is a geometric object that exists intrinsically on the manifold, it is coordinate-independent. $dx(v)$ is a representation of this object $v$ using $x$-coordinate. 

Because $x$ is a coordinate, we introduce the notation ${\partial}/{\partial x_i}$ as the tangent vector pointing the $x_i$ direction. Geometrically, for example, $\partial / \partial x_1$ represents the velocity of a curve where only $x_1$ is changing:
$$
\gamma(t)=\left(x_1+t, x_2, x_3, \ldots, x_n\right)
$$
The tangent vector to this curve is $\partial / \partial x_1$.

Back to the general idea: $dx(v)$ is a representation of $v$ in x-coordinate. How do we represent $v$ using $dx(v)$? 
We use tangent vector ${\partial}/{\partial x_i}$ as the basis (it's feasible because each $x_i$ is independent),  component $dx_i(v)$ as the coefficient. 

Remember $dx(v)$ is a representation of $v$, their information content is the same. The vector $v$ and its components $[dx_1(v),dx_2(v),dx_3(v)\cdots dx_n(v)]$ contain equivalent information. We can reconstruct $v$ from its components:
$$
v=d x_1(v) \frac{\partial}{\partial x_1}+d x_2(v) \frac{\partial}{\partial x_2}+\cdots+d x_n(v) \frac{\partial}{\partial x_n}=\sum_i^n d x_i(v) \frac{\partial}{\partial x^i}
$$

Here, $dx_i(v)$ is the speed of $v$ in $x_i$ component, ${\partial}/{\partial x_i}$ is the direction of $v$ in $x_i$ component.

Recall $v$ is an intrinsic vector, so it's coordinate-independent; if $f$ is a (smooth) function, $v[f]$ means the speed (scalar, real number) of $f$ if we move along $v$, it's called the directional derivative of $f$ along $v$. Another notation of $v[f]$ is $df(v)$, they are exactly the same meaning. 

For $f=f(x)$, the differential $df$ is:
$$
d f=\frac{d f}{d x} d x
$$
**Caveat**:  $\frac{d f}{d x}$ is not a fraction, it's not a cancellation in $\frac{d f}{d x} d x$. Instead, $df/dx$ is defined as the unique scalar function such that:
$$
d f=\left(\frac{d f}{d x}\right)\cdot d x.
$$
We will further explain it later.

Now apply both sides to $v$ :
$$
d f(v)=\frac{d f}{d x} \cdot d x(v)
$$
holds for every vector $v$ , then we can drop the $v$ and write:
$$
d f=\frac{d f}{d x} \cdot d x
$$
This is like in linear algebra: if two linear maps give the same output for every input, they are the same map.
And  $f^\prime(x)$ is just another notation for $df/dx$, we get the common equation in calculus:
$$
d f=f^{\prime}(x) d x
$$

## An example
For example, $f=x^2+y^3$, in this case $f$ is a smooth map:
$$f:\mathbb{R}^2\rightarrow\mathbb{R}$$
but not a coordinate map.
For $\mathbb{R}^2$, the coordinate map is simply:
$$
\begin{aligned}
& (x, y): \mathbb{R}^2 \rightarrow \mathbb{R}^2 \\
& p \mapsto(x(p), y(p))
\end{aligned}
$$
which is the identity map. Because each point is already labeled by its coordinates.
Then $df=2xdx+3y^2dy$ is the changing rate of $f$ in 2d Euclidean space. 
We choose $p=(2,3)\in\mathbb{R}^2$, at this point, the $df$ becomes:
$$
\left.d f\right|_{(2,3)}=2(2) d x+3(3)^2 d y=4 d x+27 d y
$$
Then we choose a tangent vector. (In Euclidean space any vector is a tangent vector, but other non-trivial spaces, e.g. $S^2$, we must choose vectors tangent to the sphere). Pick any vector, say $v=1 \partial / \partial x+2 \partial / \partial y$.
Apply $v$
$$
d f(v)=4 \cdot d x(v)+27 \cdot d y(v)=4(1)+27(2)=58
$$
It means: in $\mathbb{R}^2$ space has a function $f=x^2+y^3$, at the point $p=(2,3)\in\mathbb{R}^2$, if we move along the vector $v=1 \partial / \partial x+2 \partial / \partial y$, the function $f$ changes at rate 58.

# Caveat in calculus: 
In informal calculus, people write things like:
$$
\frac{d y}{d x}=f^{\prime}(x) \quad \Rightarrow \quad d y=f^{\prime}(x) d x
$$
and say "multiply both sides by dx."
But this isn't algebraic multiplication! 
The first $\frac{d y}{d x}=f^{\prime}(x)$ is just notation. Then we (algebraically) multiple $dx$ to both side: 
$$\left(\frac{d f}{d x}\right)\cdot d x=f^\prime(x)\cdot dx$$
By definition 
$$\left(\frac{d f}{d x}\right)\cdot dx=df$$
Thus 
$$df=f^\prime(x)dx$$
Why do this? Because $f^{\prime}(x)(v)$ is undefined.
Now we can apply both sides to a vector $v$:
$$
d y(v)=f^{\prime}(x) \cdot d x(v)
$$
to calculate the changing rate of $f$ in vector $v$. 













