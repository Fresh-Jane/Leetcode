### Implement a k-means clustering algorithm for unsupervised learning in Python

```
import numpy as np

class KMeans:
    def __init__(self, n_clusters, max_iter=100):
        self.n_clusters = n_clusters
        self.max_iter = max_iter
    
    def fit(self, X):
        n_samples, n_features = X.shape
        
        # Initialize centroids
        idxs = np.random.choice(n_samples, self.n_clusters, replace=False)
        self.centroids_ = X[idxs]
        
        # Iterate until convergence or max_iter
        for i in range(self.max_iter):
            # Assign clusters to data points
            labels = self._assign_labels(X)
            
            # Update centroids
            old_centroids = self.centroids_
            self.centroids_ = self._update_centroids(X, labels)
            
            # Check for convergence
            if np.allclose(self.centroids_, old_centroids):
                break
    
    def predict(self, X):
        return self._assign_labels(X)
    
    def _assign_labels(self, X):
        # Calculate distances to centroids
        distances = np.sqrt(((X - self.centroids_[:, np.newaxis])**2).sum(axis=2))
        
        # Assign data points to closest centroid
        return np.argmin(distances, axis=0)
    
    def _update_centroids(self, X, labels):
        centroids = np.zeros((self.n_clusters, X.shape[1]))
        for k in range(self.n_clusters):
            centroids[k] = np.mean(X[labels == k], axis=0)
        return centroids

```
