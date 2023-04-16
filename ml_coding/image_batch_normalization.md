### Implement image batch normalization 


```
The forward method takes a batch of images as input (X) and normalizes it, then returns the normalized batch of images (X_norm).

The backward method takes the gradients of the loss with respect to the normalized batch of images (dY) as input and returns the gradients of the loss with respect to the original batch of images (dX). This method is used during backpropagation to compute the gradients that will be used to update the parameters of the model.

```

```
import numpy as np

class ImageBatchNormalization:
    def __init__(self, epsilon=1e-8):
        self.epsilon = epsilon
        self.mean = None
        self.variance = None

    def forward(self, X):
        self.mean = np.mean(X, axis=(0, 2, 3), keepdims=True)
        self.variance = np.var(X, axis=(0, 2, 3), keepdims=True)
        X_norm = (X - self.mean) / np.sqrt(self.variance + self.epsilon)
        return X_norm

    def backward(self, dY):
        N, C, H, W = dY.shape
        X_mean = np.mean(dY, axis=(0, 2, 3), keepdims=True)
        X_var = np.var(dY, axis=(0, 2, 3), keepdims=True)
        X_mu = dY - X_mean
        X_std_inv = 1 / np.sqrt(X_var + self.epsilon)
        dX = (1. / (N * H * W)) * C * X_std_inv * (N * H * W * dY - np.sum(dY, axis=(0, 2, 3), keepdims=True) - X_mu * X_std_inv ** 2 * np.sum(X_mu, axis=(0, 2, 3), keepdims=True))
        return dX

x = [[[[1,1,1],[1,5,1],[1,1,1]], [[2,2,2],[3,7,2],[2,2,2]]], 
     [[[1,1,1],[1,5,1],[1,1,1]], [[2,2,2],[3,7,2],[2,2,2]]]]
x_array = np.array(x)
#print (x_array.shape)
image_bn = ImageBatchNormalization()
x_norm = image_bn.forward(x_array)
#print (x_norm)
```
