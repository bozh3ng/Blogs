
*Brief introduction to intrinsic and extrinsic perspectives*

---

## Prologue: What defines a person?
This article originated from a conversation I had with a friend: How should we treat human rights? In philosophy, Kant argued that rational human beings should be treated as an end in themselves, not as a means to something else: a person has inherent dignity. Marx saw it differently: a human being is a socially constructed, creative species-being (Gattungswesen) whose nature is defined by productive labor and social relations. The self is constituted by its surroundings, by its embedding in a social world.

Even though it is controversial, if we let our analogy run wild, there are mathematically two ways of understanding the same object: *intrinsic* and *extrinsic*. At least in mathematics, neither is more correct than the other; they are just different representations of the same reality. 

What follows is a tour of this idea. I start from a confusion I had when I was a child.


## Sailing around the world

In 1522, the remnants of Magellan's expedition completed the first circumnavigation of the globe. They had demonstrated that the Earth is not "flat" (technically closed in at least one direction) — you can go all the way around.

![[file-20260409162156959.svg]]

But this doesn't prove the Earth is a sphere! How do we know we're not living on a donut? The easiest (maybe not) way to determine this is to take a picture from space. But obviously people had already determined the shape of the Earth before that. If not by circumnavigation, then how?

Unfortunately, the answer to this question is not as easy as it looks, and we are not prepared to discuss it here.

But it's definitely doable, even though we don't introduce how yet. Taking a picture from space and traveling on the surface of the Earth are equivalent ways to know our Earth, corresponding to extrinsic and intrinsic. They both have the full ability to describe an object (not necessarily geometric).  

## Intrinsic and Extrinsic

Extrinsic lives with ambient space. "Ambient" just means "surrounding." An ambient space is just a larger space that an object fits in. For example we put a sphere in a 3D Euclidean space so we can parameterize it. The extrinsic view needs ambient space, contingent on the choice of ambient space. 

But one fact we must accept: an object exists by itself, ambient space is not necessary for the existence of an object. A sphere is always a sphere whether we put it in 3D Euclidean space, or a distorted high-dimensional space, or no space at all. This is the view of intrinsic. 

Roughly, intrinsic properties are determined by the object itself. Extrinsic describes the relationship between the object and its ambient. 

## Two pictures of gravity

In this section we briefly introduce Einstein's general relativity and Newton's perspective (not Newton's law) to explain gravity. The distinction between intrinsic and extrinsic is not just a mathematical curiosity. It sits at the center of one of the great transitions in physics: from Newton's picture of gravity to Einstein's.

In Newton's picture, space and time are a fixed, flat stage, an absolute backdrop against which physics unfolds. Space is Euclidean, time flows uniformly, and neither is affected by what happens within them. A planet moves through this stage, and gravity is a *force* that reaches across it and pulls objects off their natural straight-line paths. This is, at its heart, an *extrinsic* viewpoint: everything is observed against a fixed ambient background, and gravity is a deviation from flatness.

Einstein replaced this entirely with an *intrinsic* picture. In general relativity, there is no fixed stage. Space and time are not a passive backdrop but a dynamic, curved entity, *spacetime*, shaped by the distribution of mass and energy through the Einstein field equations. A planet does not sit *in* spacetime the way a ball sits in a box. The planet and the spacetime around it form one geometric structure.

In this picture, gravity is not a force. Objects in free fall, including light, follow geodesics: the straightest possible paths through curved spacetime. Light curving near a star is not being "pulled" off a straight line. It is traveling as straight as it possibly can. The apparent bending is an artifact of projecting a curved geometry onto flat expectations. There is a famous quote by John Archibald Wheeler "Matter tells spacetime how to curve, spacetime tells matter how to move."

![[file-20260409162156961.png]]


## Two pictures of kernel 

In machine learning, given two points $x,y$, the kernel $k(x,y)$ measures how correlated the function values $f(x)$ and $f(y)$ are. If $k(x, y)$ is large: knowing $f(x)$ tells you a lot about $f(y)$ . If $k(x, y)$ is near zero: $f(x)$ and $f(y)$ are roughly independent.
Sometimes the kernel itself has some contraints. For example in Gaussian Process context, the kernel must be covariance function, $k(x,y)=\operatorname{cov}(f(x), f(y))$ . Because the kernel defines the joint Gaussian distribution over function values.

The usual distance-based formula of SE kernel 
$k(x, y)=\sigma^2 \exp \left(-\|x-y\|^2 / 2 \ell^2\right)$
is an extrinsic view. This relies on measuring distance between pairs of points

$C(x, y):=\operatorname{cov}(Z(x), Z(y))=\mathbb{E}[(Z(x)-\mathbb{E}[Z(x)])(Z(y)-\mathbb{E}[Z(y)])]$.

Operator-based definition (intrinsic): $e^{-\frac{\kappa^2}{4} \Delta} f=\mathcal{W}$
This defines the kernel through a differential operator acting on the space itself. The Laplacian is defined purely from the local geometry - it doesn't need distances between pairs of points or any embedding into $\mathbb{R}^n$. It only needs the metric tensor at each point.

So the extrinsic view asks "how far apart are these two points?" while the intrinsic view asks "what does smoothing look like on this space?" Both give the same kernel on $\mathbb{R}^n$, but the intrinsic view generalizes to any Riemannian manifold because the Laplace-Beltrami operator is always well-defined from the metric alone.

This parallels the gradient story from earlier - the Euclidean gradient is an extrinsic object, but $\operatorname{grad} f=G^{-1} \partial f$ redefines it intrinsically through the metric, making it generalizable to any manifold.
## Coda

Modern mathematics has decisively embraced the intrinsic viewpoint as foundational. A Riemannian manifold is defined by its metric, not by any embedding. Spacetime in general relativity has no ambient space. The intrinsic perspective is more general and more honest about what the geometry actually depends on.

But when we need to calculate, to visualize, to connect abstract structures to concrete experience, we reach for the extrinsic. We draw surfaces in three-dimensional space. We choose coordinates. We embed the abstract into the familiar.


