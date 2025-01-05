
## Machine Learning
- Predictions dependent on nature of data
	- Matrix algebra is used to represent data
- Main goal is to identify patterns in data and make predictions based on future data

## Support Vector Machines (SVM)
- Hyperplane: A subspace of one dimension less than the dimensional of the full space. Acts as a decision boundary
	- The best one has maximum distance from both classes
- Support vectors: points that are closest to the hyperplane
- Margin: the distance between the hyperplane and observations closest to the hyperplane (support vectors)
	- Larger margins are better, since they imply a greater distinction between the categories effectively reducing misclassifications
	- Goal of SVMs is to maximize margins

## Principal Component Analysis (PCA)
- Used for dimensionality reduction
- Reduces the number of parameters so that no parameters are redundant and to limit the noise in the dataset
- Higher eigenvalues in a centered dataset acquired from the eigenvectors of the covariance matrix implies more variance 
- Can help identify feature importance too
- Speeds up computation too by reducing the number of parameters
- Usually done before training your model

## Train/Test Splits and Overfitting
- Common Ratio: 70:30
- **Validation set**: subset of data to tune model hyperparameters and prevent overfitting before final evaluation on the test set
- **Hyperparameter**: Chosen setting before training the model, regarding, for example, speed of training or overall complexity
- **Overfitting**: Performs very well on the training data, but fails to generalize 
- Test set is used for the final evaluation

## Other Terms
- **Confusion Matrix**: stores true positives, false positives, true negatives, and false negatives
- `Accuracy = (True Positives + True Negatives) / Total Predictions`
- `Precision = True Positives/(True Positives + False Positives)`
- **Mean squared error:** important for regression


