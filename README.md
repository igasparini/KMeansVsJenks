# KMeansVsJenks
Comparison of the KMeans and Jenks Natural Breaks clustering algorithms on some geospatial rainfall data.

## Setup:

Navigate to the project folder in the terminal and run the setup file to create an env with the dependencies.
```
./setup.sh
```

## Explanation

K-means and Jenks natural breaks are two clustering algorithms with different objectives:

- K-means minimizes the sum of squared Euclidean distances between data points and cluster centers:

  $C = \sum_{j=1}^{k} \sum_{x\in S_j} dist(x, c_j)$

  where $x$ is a data point in cluster $S_j$, and $c_j$ is the center of cluster $S_j$.

- Jenks natural breaks minimizes the sum of absolute deviations between data points and cluster centers:

  $J = C - \sum_{j=1}^{k-1} dist(c_{j+1}, c_j)$

The key difference is that K-means uses squared Euclidean distance, while Jenks uses absolute deviation. This means K-means prioritizes minimizing the distance between data points and cluster centers, while Jenks adds a penalty for the proximity between cluster centers themselves, preferring more separated clusters even if they are internally less compact.

![Clustering Animation](clustering.gif)

*Animation showcasing the iterative process of K-means clustering.*

Note: The source mentions Euclidean distance for Jenks, but other references suggest it uses absolute deviation. Corrections and clarifications are welcome.

