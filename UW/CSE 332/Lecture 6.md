## Amortization
- Equally distribute cost across all periods of application
- In an algorithmic context, if an operation is usually pretty efficient and rarely expensive, we can distribute the cost of that expensive case over all inexpensive cases. This gives us a better idea of the cost of that operation, rather than looking at the worst possible case that's not going to occur very frequently
- Use case depends heavily on the situation
- Useful for examining the cost of a series of operations. If you're looking at just one, it makes more sense to look at the absolute worst case scenario. 

## Amortization vs. Case Analysis
- Amortized answers: Am I looking at one operation or a sequence of operations?
- Case Analysis: Based on some state, how long could one operation take? Focus on inputs.

## Recursive Code Analysis
* Write a recurrence
* Tree Method
	* Draw out a tree for each recursive call
	* Add up all the work across all recursive calls
* Recursive Work = $\sum_{i=0}^{\text{last recursive level}} NumNodes(i) \cdot WorkPerNode(i)$
