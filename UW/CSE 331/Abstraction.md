## Procedural Abstraction
- Hide the details of the function from the caller
- Caller promises to pass valid inputs (adhere to the precondition)
- Implementer promises to return correct outputs (adhere to the postcondition)
- Other properties: easy to change, easy to understand, modular
	- Abstraction helps realize all of these
- Can think of a specification as a barrier between client and function implementation

**Abstraction Function**: Defines what abstract state the field values currently represent
- Relates obj to this
**Representation Invariant**: 
-  Facts about the field values that should always be true
- Defines what field values are allowed
- AF only needs to apply when RI is true
- Doesn't talk about obj

**Constructor**
- AF + RI should hold after, not before

**Methods**
- AF + RI hold at the beginning and the end





