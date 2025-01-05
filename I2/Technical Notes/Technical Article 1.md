## Data Splitting
- Train model only on some of the available data (typically 70 or 80 percent) and validate its efficacy on the rest 
- This is done to prevent overfitting to the training set and to ensure that the model can generalize well to new data
- Common workflow
	- Step 1: Data splitting
	- Step 2: Model training
	- Step 3: Model evaluation
- Validation sets are also used to train hyperparameters 

## Regression and Classification Tasks
- Machine learning typically tackles either classification or regression
- Classification:
	- Categorize input into a set of predefined classes
- Regression: predicting a continuous value based on some inputs

## Fundamentals of Linear Regression
- Tries to model the relationship between the input features and the target output by fitting a straight line to the data points
- General form:
$$\hat{y} = b  + \hat{w}\cdot \hat{x}$$
- w is the weights of the model, y is the vector containing the outputs, and x is the input
- End goal is to find values of b and w that minimize the discrepancy between the predicted and actual outputs

## Sum of Squared Errors (SSE)
- Metric to identify how well a model fits the observed data
- Sums the square of the difference between actual and predicted values
	- the squaring ensures all differences contribute positively to error, i.e., so that negative differences don't reduce the error
- Formula:
$$\text{SSE} = \sum_{i = 1}^{m} (y_i - \hat{y_i})^2$$
- $y_i$ is the actual value, while $\hat{y_i}$ is the predict value, m is the number of data points in the dataset
- Goal is to minimize SSE

## Minimizing SSE
- Simplest regression example:
$$\hat{y} = w_0 + w_1 x$$
- To minimize the SSE of this equation, we take partial derivatives of the SSE with respect to the weights and set the derivative equal to zero
- Doing this, we get the following equations:
$$w_0 = \frac{\Sigma y - w_1\Sigma x}{n}$$
$$w_1 = \frac{\sum(x_i - \bar{x})(y_i - \bar{y})}{\sum(x_i - \bar{x})^2}$$
## Fundamentals of Logistic Regression
- Used to predict a binary outcome (either 1 or 0)
- Uses a sigmoid function to transform the output of a linear equation into a probability between 0 and 1
- Sigmoid Function formula:
$$P(y = 1 | x) = \frac{1}{1 + e^{-(b + w^{T}x)}}$$
	- $w$ is the vector containing all weights. $w^{T}x$ is equivalent to taking the dot product of $w$ and $x$
	- $b$ is the bias term
- Behavior of the sigmoid function
	- If the result of the linear operation is a large number, the sigmoid function will output something close to 1
	- If the result a large negative number, the sigmoid function outputs a value close to 0
	- If the result is near 0, the sigmoid function outputs roughly 0.5
- Loss function to minimize is log-likelihood loss
- To extend to multi-class classification, we use a one-vs-rest approach, using several logistic regression models designed to classify one class. The final output is decided by which of the outputs of these models is the highest


## Intro to Unsupervised Learning
- Operates on unlabeled data and aims to find hidden patterns or structures within it
- K-means clustering does just this, grouping data points into k clusters

## K-Means Clustering 
- Operates by recalculating the center of each cluster, known as the centroid, Main goal is to minimize the distance between data points and their corresponding centroids 
- Step 1: Initialization. Selects $k$ initial cluster centroids from the dataset. The centroids act as starting points for the clusters
- Step 2: Assignment. Each data point is assigned to the nearest centroid based on Euclidean distance
- Step 3: Update. Centroids are updated based on all the data in the cluster
- Step 4: Repeat. We repeat steps 2 and 3 until the centroids converge

## Minimizing Within-Cluster Distance
- Goal of K-means is to minimize the distance between the data points and the centroid of their assigned cluster
- Equation is the following:
$$\text{SSE} = \sum_{j = 1}^{k} \sum_{x_I \in C_j} ||x_i - \mu_j||^2$$
	- $x_i$ is a data point
	- $u_j$ is the centroid of cluster j
	- $C_j$ represents the set of points assigned to cluster j

## Choosing a value for K
- Number of clusters is not known in advance
- Elbow method: The "elbow" point on the k-SSE graph indicates the optimal value for k

## Limitations of K-means
- Sensitivity to initialization: Bad initializations can result in suboptimal clusters or can cause the algorithm to converge to a local minimum
- Fixed number of clusters: Number of clusters is not always clear, which adds complexity
- Sensitivity to outliers: K-means is significantly impacted by outliers as it considers each data point equally in the calculation of its centroids

## K-Medians Clustering
- Calculates the median of the data points instead of the mean
- Less impacted by outliers
- Tries to minimize the sum of absolute differences
- When to use:
	- Dataset contains outliers
	- Mean is unreliable or heavily influenced by the values of the data points
- This is less computationally efficient than K-means, but more resilient when dealing with noise

## Bias-Variance Tradeoff
- Relates to overfitting and underfitting
- Bias refers to how close the model line is to the true underlying curve 
- Variance refers to the robustness or expressitivity (relates to complexity) of the model
- Goal is to minimize bias and variance

## Convexity
- Convex functions have one, clear global minimum.
- When dealing with non-convex functions, you cannot be sure that the minimum you found through training is the global minimum
![[Pasted image 20241015145943.png]]


