- Ignore constant **factors** - not exponents
- If you have something like $n^2 + n$ in the exponent (like $2^{n^2 + n}$), you can write $2^{(O(n^2))}$

## Big-O Formal Definition
- $f(n$) is $O(g(n))$ is there exist positive constants c, $n_0$, such that for all $n \geq n_0$, $f(n) \leq c \cdot g(n)$
- Use the tightest  Big-O bound

## O, Omega, Theta
- Big O is an upper bound
- Big Omega is a lower bound
	- $f(n$) is $\Omega (g(n))$ is there exist positive constants c, $n_0$, such that for all $n \geq n_0$, $f(n) \geq c \cdot g(n)$
- Big Theta is "equal to"
	- $f(n$) is $\Theta(g(n))$ if $f(n)$ is $\Omega (n)$ and $O (n)$.
- All of these can be defined as a set of functions that meet the provided requirements

## Proving Big-O Formally
- Big O proof is an exists statement and a forall