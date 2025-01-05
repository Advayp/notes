## Network Structure
- Hierarchical structure composed of several layers
- Primary layer of neurons is called the input layer (single-column vector)
	- Inputs, such as images or audio, are converted to vectors prior to training
- NNs also contain hidden layers, which add non-linearity to the NN and allow it to fathom more complex patterns
- Last layer is called the output layer, which encodes the solution to the problem the NN is trying to solve

**Some benefits of networks**: No feature engineering is required due to the complexity of an NN, enabling it to capture more robust and elusive patterns

## Flow of Information
- Each connection between a pair of neurons has a weight ($w$) and a bias ($b$)
	- The bias determines how sensitive a neuron is to the input and changes in the input
- The diagram below illustrates how the weights and outputs of previous layers are conceptually used to compute the value of one output in the current layer
![[Pasted image 20241026161848.png]]
- In practice, forward propagation is implemented using matrix multiplication and other vector operations
- The formula is the following
$$\vec{l_{n + 1}} = W_{l}\vec{l_n} + \vec{b_{n + 1}}$$
- Where...
	- $\vec{l_{n + 1}}$: The values stored in the $(n + 1)^{th}$ layer (the yellow layer in the diagram above)
	- $W_l$: The matrix containing the weights to go from layer $n$ to $n + 1$
	- $\vec{l_n}$: The values of the previous layer (the pink layer in the diagram above)
	- $\vec{b_{n +1}}$: The biases associated with the current layer

## Non-linearity and Activation Functions
- Complexity is only introduced when non-linearity is present, as the range of functions that we can approximate increases drastically when we implement the latter
- To implement non-linearity, models use activation functions
- Some common activation functions:
![[Pasted image 20241026162929.png]]
- Change the impact certain neurons have on the overall results of the NN
- These functions are applied after computing the raw values (i.e., after the matrix multiplication and the vector addition of the biases)
	- Side note: those raw values are called logits


## Backpropagation
- Process that adjusts each of the weight matrices assigned to each layer to improve the performance of the neural network
- Loss function measures the discrepancy between the model's predicted values and ground truth
	- For regression, mean squared error (MSE) is a commonly-used loss function
	- For classification problems, cross entropy loss (aka log loss) is mostly used
		- Formula: $$L = -\frac{1}{N} \sum_{i = 1}^N \sum_{k = 1}^K y_{ik} \log(\hat{y_{ik}})$$
			- $N$: Number of training samples
			- $K$: Number of classes
			- $y_{ik}$: Expected output
			- $\hat{y_{ik}}$: Predicted output


## Optimizers
- Main goal is to reduce the calculated loss
- **Gradient Descent**: Computes the gradients for each set of weights at every step and then adjusts them based on that gradient, moving toward a local minima
- **Stochastic Gradient Descent** **(SGD)**: Very similar to gradient descent, but updates data in batches 
- **Adam**: Combines SGD and another technique called Momentum, which helps the model's weights approach a local minimum faster
- Learning Rate, a parameter referenced by each of these optimizers, determines how much to change the weights by during each epoch. 

## Regularization
- At the basic level, we add a norm to the loss function, which encourages weights to reach other smooth (L2) or sparse (L1) optima
- **Dropout**: During each iteration, a fraction of the neurons are temporarily dropped from the neural network 
	- Dropped weights have no impact during forward propagation and are not changed during backpropagation 
	- Dropping only occurs during training time. During test time, all neurons are used
	- Ensures all the neurons are used to their fullest potential, implying more robustness
	- Smaller implementation detail: all neurons have their weight scaled by 1 minus the dropout rate
- **Batch Normalization**: An extra layer with very few parameters. This layer sits among hidden layers, and mathematically normalizes the data across examples in the batch
	- After normalizing, data is also scaled ($\gamma$) and shifted ($\beta$) before it's passed on to the next layer
