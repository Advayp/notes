## Backwards Reasoning
- Fill in precondition from postcondition
- Given S (code) and Q (post condition), find P (precondition)
- Generally want the weakest precondition, one that allows the most states
	- For this reason don't copy facts backwards
- Conditionals are handled using proof by cases. Branches are OR'd together
- Early returns
	- Check if post condition holds
	- After the if statement though, we know for a fact that the condition in that branch isn't true


## Loop Invariants
- Invariant: True every time at the top of the loop
- Must remain true each time you execute the body of the loop
- Split into three parts
	- Invariant holds initially
	- S preserves I
	- Q holds when loop exits