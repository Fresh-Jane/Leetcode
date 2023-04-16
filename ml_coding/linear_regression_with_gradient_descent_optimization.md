### linear regression model using gradient descent optimization

Implement a linear regression model using gradient descent optimization.

```
import numpy as np

class LinearRegression:
    def __init__(self, lr=0.01, n_iters=1000):
        self.lr = lr
        self.n_iters = n_iters
        self.weights = None
        self.bias = None
    
    def fit(self, X, y):
        # Initialize weights and bias
        n_samples, n_features = X.shape
        self.weights = np.zeros(n_features)
        self.bias = 0
        
        # Gradient descent optimization
        for _ in range(self.n_iters):
            y_pred = np.dot(X, self.weights) + self.bias
            dw = (1/n_samples) * np.dot(X.T, (y_pred - y))
            db = (1/n_samples) * np.sum(y_pred - y)
            self.weights -= self.lr * dw
            self.bias -= self.lr * db
    
    def predict(self, X):
        y_pred = np.dot(X, self.weights) + self.bias
        return y_pred
```
```
In this example, we define a class LinearRegression that contains methods for fitting the model to the data using gradient descent optimization and making predictions using the learned weights and bias.

The fit() method initializes the weights and bias to zero and performs gradient descent optimization for a fixed number of iterations. In each iteration, the predicted values y_pred are calculated using the dot product of the input features X and the weights, and the bias is added. Then, the gradient of the loss function with respect to the weights and bias is computed, and the weights and bias are updated by subtracting the learning rate multiplied by the gradient.

The predict() method uses the learned weights and bias to make predictions on new data by computing the dot product of the input features X and the weights and adding the bias.

To use this implementation, you can create an instance of the LinearRegression class and call the fit() method on your training data to learn the weights and bias, and then call the predict() method on your test data to make predictions.
```
