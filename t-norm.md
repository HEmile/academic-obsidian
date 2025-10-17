---
aliases:
- "triangular subnorm"
- "triangular norm"
- "t-subnorm"
- "idempotent element"
- "nilpotent element"
- "zero divisor"
isA:
- "[[fuzzy operators]]"
- "[[associative]]"
- "[[ordered semigroup]]"
---
	
> [!definition]
> Axioms: $T: [0, 1]^2 \rightarrow [0, 1]$
> - [[commutative|commutativity]] $T(x, y)=T(y, x)$
> - [[associative]]
> - [[monotonicity]]
> - Boundary: $T(x, 1)=x$

Implies: $T(x, 0) = 0$, $T(x, y) \leq \min(x, y)$. 

There are also **triangular subnorms**, for which the Boundary doesn't hold, but $T(x, y) \leq \min(x, y)$ does. 

## Analytical elements
> [!definition]
> **Idempotent element** is $a$ st $T(a, a)=a$. 
> **Nilpotent element** is $a$ st there is some $n$ st $T(a, ..., a)=0$ (take $n$ times)
> **Zero divisor** is $a$ st there is some $b\in(0, 1)$ st $T(a, b)=0$. 

## Properties
- If $\phi:[0, 1]\rightarrow [0, 1]$ is a [[strictly inc]] [[bijectivity|bijection]], then $T_\phi(x, y)=\phi^{-1}(T(\phi(x), \phi(y)))$ is also a t-norm, and forms an [[isomorphism]] with $T$ through $\phi$. 
 
--- 
#concept
Created [[17-03-2021]] at 11:21