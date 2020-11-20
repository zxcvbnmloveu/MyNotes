# `numpy实现kmeans`

```python3
import numpy as np
import matplotlib.pyplot as plt
from sklearn.utils import shuffle

'''
kmeans training steps:

S1:
init k cluster (k,fea_dim)

s2:
assign labels to all training samples

s3:
recalculate cluster center[i] = x[label==i].mean(1)

iteration end for max_iter or k_center unchange
'''

class my_kmeans:
    '''

    '''
    def __init__(self,k_cluster,n_iters):
        self.k_cluster = k_cluster
        self.n_iter = n_iters
        self.centroids = None

    def initial_centroids(self,x,k):
        # simplest 随机选K个样本点当作初始点
        # init_indice = np.random.randint(0, x.shape[0], self.k_cluster)
        # self.centroids = x[init_indice]

        # kmeans++
        #**gradually select centers, criterion: sum of dises between cur_sample and cur_centers.
        self.centroids = np.array([x[0]])
        for j in range(k-1):
            for i,centroid in enumerate(self.centroids):
                d = np.sqrt(np.sum((x - centroid)**2,1))
                if i == 0:
                    dist = d
                else:
                    dist += d
            self.centroids = np.concatenate((self.centroids,[x[dist.argmax(0)]]),0)


    def fit(self,x):

        # initial
        self.initial_centroids(x,self.k_cluster)
        cnt = 0
        change_flag = True
        print(self.centroids)
        while cnt < self.n_iter and change_flag:
            # predict
            label = self.predict(x)
            # update
            new_centroids = np.array([x[label==i].mean(0) for i in range(self.k_cluster)])
            if (new_centroids == self.centroids).all(): change_flag = False
            self.centroids = new_centroids


    def predict(self,x):
        try:
            for i,centroid in enumerate(self.centroids):
                d = np.sum((x - centroid)**2,1).reshape(-1,1)

                if i == 0:
                    dist = d
                else:
                    dist = np.concatenate((dist,d),1)

            label = dist.argmin(1)

            return label
        except:
            assert 'kmean is not initialized'

# 测试代码
x1 = np.random.rand(100,2)*0.3+np.array([0.3,0.3])
x2 = np.random.rand(100,2)*0.3+np.array([0.5,0.5])
x3 = np.random.rand(100,2)*0.3+np.array([0.3,0.6])
x4 = np.random.rand(100,2)*0.3+np.array([0.7,0.2])

x = np.concatenate((x1,x2,x3,x4),0)
y = np.array([0]*100+[1]*100+[2]*100+[3]*100)
x,y = shuffle(x,y)

mks = my_kmeans(k_cluster=4,n_iters=3)
mks.fit(x)

c = mks.centroids
plt.figure(1)
plt.scatter(x[:,0],x[:,1],s=5)
plt.scatter(c[:,0],c[:,1],marker='*',s=500)
plt.show()

plt.figure(2)
label = mks.predict(x)
v1 = x[label==0]
v2 = x[label==1]
v3 = x[label==2]
v4 = x[label==3]
plt.scatter(v1[:,0],v1[:,1],s=5)
plt.scatter(v2[:,0],v2[:,1],s=5)
plt.scatter(v3[:,0],v3[:,1],s=5)
plt.scatter(v4[:,0],v4[:,1],s=5)
plt.show()
```

#### 形心

<img src = 'https://i.bmp.ovh/imgs/2020/11/b4bcf6125e625590.png'/>

#### predict

<img src = 'https://i.bmp.ovh/imgs/2020/11/f99f88b5a04f3836.png'/>
