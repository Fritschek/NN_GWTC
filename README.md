# NN_GWTC
Simulations for the paper "Deep Learning for the Gaussian Wiretap Channel" with Tensorflow 2

Requirements: The code needs a package for an equal cluster-size version of K-Means.
I am using the code from https://github.com/ndanielsen/Same-Size-K-Means for that.
Note that newer versions of K-Means/Sci-kit learn require that the fit function of the original k-means
gets a sample_weight vector. This leads to breaking changes within the same-size kmeans code. 
A quick fix is to introduce a uniform sample weighting via:

        n_samples_var = X.shape[0]
        sample_weight = np.ones(n_samples_var, dtype=X.dtype)
       
#K-mean clustering same size k means (working)#
Same Size Clustering
This is a variation of the k-means clustering that produces equally sized clusters.

The algorithm consists of two phases:

#1. Initialization:

Compute the desired cluster size: n/k

Initialize means with k-means

Order points by the biggest benefit (delta distance) of best over worst assignment

Assign points to their prefered cluster until the cluster is full, then resort remaining
objects by excluding the clusters that are full.
#2. Refinement of clustering: This is done in an iterative fashion, until there is no change in clustering or the max number of iterations have been reached.

Interation:

    Compute current cluster means.

    For each object, compute the distance to the cluster means.

    Sort elements based on the delta of the current assignment and the alternative best 
    possible assignment, sort in descending order.

    For each element by priority:

        For each cluster to whom it doesn't belong, by element gain:

            if there is an element on the transfer list of the cluster, and swapping the 
            two element yields improvement, swap the two elements;

        End For

        If the element is not swapped, add to outgoing transfer list

    End For

    If no transfers were done, or max iteration was reached, terminate.

Since any transfer must decrease variance, thus the clustering will converge.
