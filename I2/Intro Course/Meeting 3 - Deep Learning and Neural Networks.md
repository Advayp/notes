## Deep Learning
 - Advanced subset of machine learning and AI
 - Requires a lot more computational intensity and is more involved from a resources standpoint

## Conceptual definition
- Data-based function approximator
- A neural network approximates the underlying function that creates outputs from inputs
- Pattern recognizers, useful for unstructured data

## Forward Propagation
- Run it through the various layers, moving from one layer to another by using a semi-random set of weights and biases
- This is done using a matrix multiplication


## Activation Functions
- Activation functions introduce non-linearity, which adds depth to the model
- Most common for hidden layers: 
	- RELU: `max(0, x)`


## Back propagation
- Goal is to find the best weight matrices
- Randomly initialize matrices when starting 
- Loss function: mean squared error over all the examples is used to determine how incorrect the model's output is
- Loss is kept in vector form, however, for back propagation
- Gradient descent: the process of moving toward a local minima, done to optimize the values in the weight matrices
	- Done two layers at a time, enables us to move backward through the whole neural network 

## Learning Rate ($\lambda$)
- How quickly to change the value of a particular weight
- Epoch: a pass through the whole training dataset
	- Back propagation is done after an epoch
- Good learning rate ensures the loss function decreases steadily 
	- High learning rate => passing over the local minima 
	- Low learning rate => little to no improvement in the loss function
	- Typical value of $\lambda$: 0.1

## ML vs DL
- ML has guaranteed global minima, powerful models, and is more interpretable (generally better for structured data)
- DL is better for unstructured data, like text, images, and audio