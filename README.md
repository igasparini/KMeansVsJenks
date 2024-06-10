# KMeansVsJenks

Comparison of the KMeans and Jenks Natural Breaks clustering algorithms on some geospatial rainfall data of Switzerland.

## Setup

Navigate to the project folder in the terminal and run the setup file to create an env with the dependencies:

```
./setup.sh
```

## Explanation

![Clustering Animation - some suboptimal clustering is visible in the KMeans implementation for the 30-35 range.](clustering.gif)

From [Jenks natural breaks vs K-means - Cross Validated](https://stats.stackexchange.com/questions/143007/jenks-natural-breaks-vs-k-means#:~:text=The%20Jenks%20natural%20breaks%20algorithm,they%20minimize%20within%20group%20distances.):

Often Jenks is essentialy presented as a special case of k-means. However, this source makes an important distinction: K-means solely "searches for minimum distance between data points and the centers of clusters they belong to". Jenks takes this objective and adds a penalty for the proximity between the centers of clusters, and thus it also searches "for maximum difference between cluster centers themselves".

The logic is that, even if two clusters are internally very compact, they may be hard to distinguish when their centers are very close.

Thus, for n data points and k clusters, K-means would minimize C:

$$C = \sum_{j=1}^k \sum_{x\in S_j} \mathrm{dist}(x, c_j)$$

where $x$ is a data point in cluster $S_j$ and $c_j$ is the cluster center of cluster $S_j$.

In contrast, the Jenks algorithm would minimize J:

$$J = C - \sum_{j=1}^{k-1} \mathrm{dist}(c_{j+1}, c_j)$$

Jenks adds a penalty for the proximity between cluster centers themselves, preferring more separated clusters even if they are internally less compact.

The source referenced states that `dist()` computes the Euclidean distance (so, $\sqrt{(d_i - c_j)^2}$), but from everything else I read on K-means it seems that the squared Euclidean distance ($(d_i - c_j)^2$) is what is actually minimized.

Full reference:

- Khan, F. (2012). An initial seed selection algorithm for k-means clustering of georeferenced data to improve replicability of cluster assignments for mapping application. Applied Soft Computing Journal, 12(11), 3698–3700. https://doi.org/10.1016/j.asoc.2012.07.021