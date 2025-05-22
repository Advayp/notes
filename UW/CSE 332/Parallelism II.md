
## Analysis of parallel code 
- Introduce another variable P that represents the number of processors
- Let $T_p$ be the big-O running time with P processors
- We know analyze with respect to n, the input size, and P, the number of processors
- **Work**: Running time of parallel code if you had a single processor
- **Span**: Running time of parallel code as the number of processors approaches infinity
- **Speedup**: $T_1/T_p$ 
- **Parallelism**: $\frac{T_1}{T_{\infty}}$

## Amdahl's Law
$$
\frac{T_1}{T_p} \leq \frac{1}{S + \frac{1 - S}{P}}
$$
- S is the portion of the code that must be sequential
- P is the number of processors