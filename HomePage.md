bo.zheng.2020@gmail.com 
Welcome to contact me.

Nothing new is invented; I mainly focus on explaining and connecting certain concepts. Some ideas may be trivial for mathematics majors, I present them from an amateur's view.

# Summary:

[[Independence in Bayesian Network Causal Diagrams]]: Four causal structures in Bayesian Networks, analyzed through conditional probability tables. The case-by-case analysis leads to d-separation: when conditioning on a collider opens a path, and when conditioning on a non-collider blocks one.

[[AbstractAlgebra-1]]: Groups, rings, fields -- each built by adding one axiom to the last. The impossibility of dividing by zero follows from the ring axioms alone. The Euclidean algorithm is then explained through the ideal-theoretic structure of $\mathbb{Z}$.

[[Category Product]]: The categorical product is defined by a universal property with arrows pointing toward the factors. The reversed-arrow diagram defines the coproduct instead -- two arguments show they are genuinely different constructions.

[[From Distances to Coordinates(Euclidean)]]: Recovering point coordinates from pairwise distances via SVD and classical multidimensional scaling. Covers the geometry of linear maps, PSD matrices, and the double-centering trick.

[[Monoid]]: Three equivalent definitions of a monoid: set-theoretic, as a one-object category, and via commutative diagrams. The diagrammatic definition generalizes to monoid objects in any monoidal category.

[[Paradox]]: Birthday collisions (Poisson approximation), Monty Hall with an uncertain host (Bayesian synthesis of informed and random cases), Russell's paradox (axiom schema of specification), and Banach-Tarski (Axiom of Choice and free groups in $SO(3)$).

[[PCA]]: PCA as eigendecomposition of the covariance matrix, connected to SVD via $C = \frac{1}{n-1} V \Sigma^2 V^T$. The implicit assumption: signal lives in high-variance directions, noise in low-variance ones.

[[PML - From Likelihood to ELBO]]: From maximum likelihood to the ELBO, with every notational abuse made explicit. Covers the reparameterization trick, the role of the encoder as an importance distribution, and joint optimization of $\theta$ and $\phi$.

[[Probability-1]]: Measure-theoretic foundations: probability spaces, conditional probability as a restricted measure, random variables in $L^2(\Omega)$ where uncorrelated means orthogonal, and expectation as Lebesgue integration against a probability measure.

[[Product]]: A catalog of product operations across linear algebra and abstract algebra -- dot, cross, Kronecker, Hadamard, direct, free, semidirect, tensor -- with their universal properties and the distinctions that matter.

[[Semidefinite Programming and Applications]]: Semidefinite programming as the generalization of LP from $\mathbb{R}+^n$ to $S+^n$. Weak and strong duality, then applications: Euclidean distance matrix completion and sparse PCA via rank relaxation.

[[What is dx?]]: $dx$ is a 1-form that extracts directional components from tangent vectors, not an infinitesimal quantity. The differential geometry perspective, grounded with a concrete computation and the precise meaning of $df = f'(x),dx$.

[[Yoneda Perspective]]: Each natural transformation out of a representable functor is a class-indexed family, yet the Yoneda Lemma shows it is determined by a single set element. The Yoneda embedding is full and faithful -- an object is recoverable from its hom-functor.

[[Pushforward Pullback]]: Pushforward and pullback in differential geometry and probability theory. The same covariant-contravariant duality, but with the roles of "thing measured" and "measurement device" swapped -- distributions are covariant (the probability monad), observables are contravariant.

In dir Thesis:

[[Part1-PriorKnowledge]]: Every neural network component -- architecture, activation, regularization -- encodes a structural assumption about the problem before training begins. Prior knowledge constrains the model to a subspace of function space; if the prior is correct, the model searches a smaller space with less data and better generalization. This article frames the series: groups, manifolds, and categories are the formal languages for describing what is being transferred and how.

[[Part2-GroupStructure]]: A deep linear network has symmetry group $\prod_\ell \mathrm{GL}(n_\ell)$, making the map from parameters to functions wildly non-injective. Activation functions break this to specific centralizer subgroups ($\mathcal{D}^+ \rtimes S_n$ for ReLU, $S_n$ for sigmoid), and regularization breaks it further ($O_d$ for Frobenius norm, the hyperoctahedral group $B_d$ for entry-wise $\ell_p$). The hierarchy $\mathrm{GL}(n) \to \mathrm{Cent}(\sigma) \to G_{\text{reg}}$ traces how each design choice resolves the reparametrization problem and injects prior knowledge. Verified experimentally on small networks.

[[Part3-PathEquivariance]]: Classical group equivariance relates isolated points via group actions but says nothing about continuous variation through data space. Path equivariance generalizes this: $F(\gamma(t)) = a_\gamma(t) \cdot F(\gamma(0))$, requiring representations to evolve coherently along paths. The content-pose decomposition via principal bundles explains the hard/soft constraint asymmetry -- pose lives in a group (hard constraints, weight sharing), content does not (soft constraints, smoothness regularization). The hierarchy from classical to homotopy to full path equivariance measures how much geometric structure the network respects.

[[Part4-CategoryTheoryPerspective]]: Equivariance is naturality. A $G$-equivariant layer is a natural transformation between functors from $\mathbf{B}G$ to the category of representations. This identification is not merely linguistic: composition of natural transformations gives equivariance of deep networks for free, and invariant pooling is a categorical limit with a universal property. The series unifies under one principle: a model is a functor, a good layer is a natural transformation, and the design of a neural network is the choice of which structure to preserve.