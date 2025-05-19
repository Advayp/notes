
## Analysis of parallel code 
- Introduce another variable P that represents the number of processors
- Let $T_p$ be the big-O running time with P processors
- We know analyze with respect to n, the input size, and P, the number of processors
- **Work**: Running time of parallel code if you had a single processor
- **Span**: Running time of parallel code as the number of processors approaches infinity
- **Speedup**: $T_1/T_p$ 
- **Parallelism**: $\frac{T_1}{T_{\infty}}$
