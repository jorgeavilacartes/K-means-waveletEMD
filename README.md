# K-means-waveletEMD
K-means using wavelet Earth Mover's Distance

K-means is trained using [pyclustering library](https://pyclustering.github.io/).
WaveletEMD is based on wavelet transoform, using [pywavelet library](https://pywavelets.readthedocs.io)

___
## Usage
```python
import random
from src import KmeansOT
from src import WaveletEMD

# data to train the model
n_samples = 100
train_data = [[random.random() for _ in range(10)] for _ in range(n_samples)]

# train
num_clusters = 2
kmeans = KmeansOT(n_clusters=num_clusters, random_state=2)
kmeans.fit(train_data)

# test
n_test = 10
test_data = [[random.random() for _ in range(10)] for _ in range(n_test)]

# A list with cluster predictions ([0,num_clusters-1])
kmeans.predict(test_data) 
```

Information after training
```python
# Centers of each cluster
kmeans.centers

# List for each cluster, with the idx of each sample in train_data 
kmeans.clusters

# trained model
kmeans.kmeans
```

By default, the WaveletEMD is set under this configuration
```python
pywt.wavedec(wavelet = "sym5", level = 6, mode = "zero")
```

To run K-means using a different family and/or level, you must initialize K-means as shown below:
```python
# New wavelet function
wemd = WaveletEMD(wavelet = "haar", level = 2, mode = "zero") 
new_metric = distance_metric(type_metric.USER_DEFINED, func=wemd)

# Include new metric in the KmeansOT
kmeans = KmeansOT(n_clusters=num_clusters, metric = new_metric, random_state=2)
```





