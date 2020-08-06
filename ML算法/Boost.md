1. 在每一轮如何改变训练数据的权值或概率分布，修改的策略是什么？
  提高那些被前一轮弱分类器错误分类的样本的权值，而降低那些被正确分类样本的权值。这样一来，那些被分错的数据，在下一轮就会得到更大的关注。所以，分类问题被一系列的弱分类器“分而治之”

2. 如何将弱分类器组合成一个强分类器？
  对弱分类器的组合，AdaBoost采取加权多数表决的方法。即加大分类误差率小的弱分类器的权值，使其在表决中起较大作用，减小分类误差率大的弱分类器的权值，使其在表决中起较小的作用

AdaBoost算法是模型为加法模型、损失函数为指数函数、学习算法为前向分步算法时的二类分类学习算法

前向分步算法：在上一步得到的最优基函数的基础熵，极小化本次单个基函数的损失函数。

adaboost 算法过程

1）使用具有权值分布的训练数据集训练出来一个在加权数据集误差率最小的弱分类器Gm(x)

2）计算Gm(x)的误差率em

![](https://www.zhihu.com/equation?tex=%5Cbegin%7Balign%2A%7D+%5C%5C%26+e_%7Bm%7D+%3D+%5Csum_%7Bi%3D1%7D%5E%7BN%7D+P%5Cleft%28G_%7Bm%7D%5Cleft%28x_%7Bi%7D%5Cright%29+%5Cneq+y_%7Bi%7D%5Cright%29+%5C%5C+%26+%3D+%5Csum_%7Bi%3D1%7D%5E%7BN%7D+w_%7Bmi%7D+I+%5Cleft%28G_%7Bm%7D%5Cleft%28x_%7Bi%7D%5Cright%29+%5Cneq+y_%7Bi%7D+%5Cright%29+%5Cend%7Balign%2A%7D+%5C%5C)

3）计算弱分类器Gm(x)系数αm,误差约小，权重越大。西瓜树说的是em大于0.5break，所以αm是大于零的。

![](https://www.zhihu.com/equation?tex=%5Cbegin%7Balign%2A%7D+%5C%5C+%26+%5Calpha_%7Bm%7D+%3D+%5Cdfrac%7B1%7D%7B2%7D+%5Clog+%5Cdfrac%7B1-e_%7Bm%7D%7D%7Be_%7Bm%7D%7D+%5Cend%7Balign%2A%7D%5C%5C)

4) 更新训练数据集的权值分布

![](https://www.zhihu.com/equation?tex=%5Cbegin%7Balign%2A%7D+%5C%5C+%26+D_%7Bm%2B1%7D%3D%5Cleft%28w_%7Bm%2B1%2C1%7D%2C%5Ccdots%2Cw_%7Bm%2B1%2Ci%7D%2C%5Ccdots%2Cw_%7Bm%2B1%2CN%7D%5Cright%29+%5C%5C+%26+w_%7Bm%2B1%2Ci%7D+%3D+%5Cdfrac%7Bw_%7Bmi%7D%7D%7BZ_%7Bm%7D%7D+%5Cexp+%5Cleft%28-+%5Calpha_%7Bm%7D+y_%7Bi%7D+G_%7Bm%7D%5Cleft%28x_%7Bi%7D%5Cright%29%5Cright%29%2C+%5C%5C+%26+%5Cquad+%5Cquad+%3D+%5Cleft%5C%7B+%5Cbegin%7Baligned%7D+%5C+%26+%5Cdfrac%7Bw_%7Bmi%7D%7D%7BZ_%7Bm%7D%7D+%5Cexp+%5Cleft%28-+%5Calpha_%7Bm%7D+%5Cright%29%2C+G_%7Bm%7D%5Cleft%28x_%7Bi%7D%5Cright%29+%3D+y_%7Bi%7D+%5C%5C+%26+%5Cdfrac%7Bw_%7Bmi%7D%7D%7BZ_%7Bm%7D%7D+%5Cexp+%5Cleft%28+%5Calpha_%7Bm%7D+%5Cright%29%2C+G_%7Bm%7D%5Cleft%28x_%7Bi%7D%5Cright%29+%5Cneq+y_%7Bi%7D+%5Cend%7Baligned%7D+%5Cright.+%5Cquad+i%3D1%2C2%2C%5Ccdots%2CN+%5Cend%7Balign%2A%7D%5C%5C)

5) 构造分类器
![](https://www.zhihu.com/equation?tex=%5Cbegin%7Balign%2A%7D+%5C%5C+%26+G%5Cleft%28x%5Cright%29+%3D+sign%5Cleft%28f%5Cleft%28x%5Cright%29%5Cright%29%3Dsign%5Cleft%28%5Csum_%7Bm%3D1%7D%5E%7BM%7D+%5Calpha_%7Bm%7D+G_%7Bm%7D+%5Cleft%28+x+%5Cright%29%5Cright%29+%5Cend%7Balign%2A%7D+%5C%5C)
