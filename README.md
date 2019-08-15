# NN_GWTC
Simulations for the paper "Deep Learning for the Gaussian Wiretap Channel" with Tensorflow 2

Requirements: The code needs a package for an equal cluster-size version of K-Means.
I am using the code from https://github.com/ndanielsen/Same-Size-K-Means for that.
Note that newer versions of K-Means/Sci-kit learn require that the fit function of the original k-means
gets a sample_weight vector. This leads to breaking changes within the same-size kmeans code. 
A quick fix is to introduce a uniform sample weighting via:

        n_samples_var = X.shape[0]
        sample_weight = np.ones(n_samples_var, dtype=X.dtype)
       
