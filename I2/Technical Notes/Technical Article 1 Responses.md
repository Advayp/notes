## Synthesis Questions Set 1
1. Classification algorithms involve labelling inputs with either 0s or 1s, depending on their class. Logistic Regression takes in any input and reduces the set of possible outputs to between 0 and 1. This, when interpreted as probability, can enable a model to classify an input into a specific class.
2. 0

## Synthesis Questions Set 2
1. Unsupervised learning involves finding hidden structure or patterns in data. In supervised learning, each input has a "correct" output that the model must try and predict. This is different from unsupervised learning as the latter doesn't have a correct output you're trying to predict; rather, the goal is to deduce some pattern unknown to the programmer in the data.
2. A centroid is the center of each cluster in k-means clustering. It's calculated by taking the mean of all the data points in the cluster.
3. It means that the centroids have converged and that the clusters have been properly assigned.
4. 1
5. Different initializations produce different loss functions. Different loss functions have different local and global minimums, which means that in some initializations the model will converge to a local minimum instead of a global one, affecting its accuracy.

## Synthesis Questions Set 3
1. Clustering US census data
2. Identifying similar voices in an audio file
3. A regression problem, like classifying whether or not an image is a picture of a cat or a dog

## Synthesis Questions Set 4
1. Expressivity of a function refers to the complexity or robustness of the function. High expressivity means that adding new points to the dataset drastically changes the regression curve. Low expressivity means that adding new point does not affect the curve that much at all
2. High bias implies underfitting, whereas high variance implies overfitting
3. Yes. Generally speaking, low bias and low variance are qualities of a good model
4. If your problem is non-convex, you know the efficacy of your model is dependent on the initial state. This means that when dealing with non-convex problems, you can play around with different initializations to get to different minimums.
5. No, they aren't. This is because different initializations can lead to different end solutions/final centroids, which indicate the presence of multiple minimums.

