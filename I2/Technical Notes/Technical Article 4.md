## Convolutional Neural Networks
- Specific algorithm designed for computer vision 
- Tries to mimic a human's visual processing system.
- **Convolutional Layer**: These layers apply a mathematical calculation to a section of an image to extract information about that set of features. 
	- Uses a kernel, a sort of filter that amplifies and minimizes the impact of certain pixels in a given section
	- Each section gives a specific value after being processed by the kernel. This value is then stored in a new matrix.
	- To extract features from a particular section, we take the element-wise matrix product of that section and the kernel (and then the sum)
	- Mathematically, for a filter $F$ and input $I$, this looks like the following:
	$$Z(i, j) = \sum_{m = 0}^{k - 1}\sum_{n = 0}^{k - 1}\sum_{c = 1}^{C} I(i + m, j + n, c) \cdot F(m, n, c)$$
	- This returns a 2d array $Z$, which is the feature map.
	- Two other factors affect how $Z$ is created:
		- Stride: determines how many pixels the filter should shift
		- Padding: Refers to how many extra pixels should be added around the edges of a kernel. We usually pad with zeroes.
		- ![[Pasted image 20241102202526.png]]
	- The dimensions of the feature map $Z$, are the following:
		- $W_{out} = \frac{W + 2P - D \cdot (K - 1) - 1}{S} + 1$
		- $H_{out} = \frac{H + 2P - D \cdot (K - 1) - 1}{S} + 1$


## Nonlinearity in CNNs
- Non-linearity is done after using the kernel and using activation functions (just like DNNs)
- Most of the time, CNNs use ReLU as their activation function. But, this could sever certain neural connections entirely, so it's sometimes substituted with Leaky ReLU.

## Pooling Layer
- This layer effectively summarizes all the information brought out by the kernel and the convolutional layer
- Focuses on retaining significant features, while getting rid of the insignificant ones -> tries to prioritize simplicity
- One of the main goals of this is to reduce the number of parameters given to the network so that computation times are faster
- Two common techniques used when pooling:
	- Max pooling: Selects the maximum value in a given section of the feature map and lets that number represent that entire section in the summarized map
	- Average pooling: Selects the average of all values in a given section

## Fully Connected Layer
- Last layer of a CNN
- CNNs employ several convolutional and pooling layers to extract all the information from a given image 
- Input is flattened before it's passed into this layer
- Works very similar to a "normal" neural network
- This layer uses the softmax activation function to perform multi-class classification

## Loss Functions, Optimizers, and Regularization
- CNNs work very similarly to ANNs in this regard
- Loss: Cross-Entropy Loss or Mean Squared Error
- Optimization: Gradient descent or Adam
- Regularization: Dropout

## Self-Supervised Learning (SSL)
- Models are able to use unlabeled data to learn
- Goal is to generate labels for data
- A forward pass generates labels for the given data, while backpropagation shifts the weights based on some SSL-specific loss functions

## Methods of SSL
- **Contrastive Learning**: Model uses groups of data points. Similar data points are labelled "positive" while those that come from unrelated images are labelled "negative." The goal is to bring the positive pairs closer together and the negative pair further apart.
- **Predictive Tasks**: Predicts the value of certain features from those of other features. One example of a predictive task is filling in missing components of an image
- **Importance**: Labelling is often done by hand, which can be extremely tedious. SSL avoid this concern by having the model pick up directly on patterns within the data, avoiding the need for labelling entirely.

## Image Segmentation
- This focuses on identifying groups of pixels that belong together and separates objects in an image through this
- By grouping pixels, image segmentation allows for faster and more efficient image processing
- **Superpixels**:
	- One of the most important techniques used in image segmentation
	- Refers to a group of pixels that have been grouped together for a shared characteristic 
	- Each superpixel is then treated like a regular pixel, speeding up computation time
- **Things and Stuffs**:
	- Segmentation is also used to identify separate entities in images
	- "Things" are objects in images, like people, structures, etc.
	- "Stuffs" are entities that are fluid and have no characteristic shape or doesn't have countable, individual instances.
	
