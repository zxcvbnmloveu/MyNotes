# `temperature的作用`

temperature指的是分类器输出的logit的系数。正常就是为1，
这个logit有什么作用，我来推导一下。

<img src = 'https://pic1.zhimg.com/80/v2-43be1734e3d377eb1424c7fd69a23703_1440w.png' width = '600' />

因为是求和式正负不太确定，但可以看出在小于1的时候，最大的oi都会变小，最小的oi会变小。反之亦然。
这也是为什么temperature可以用作减缓收敛 [1]，或者让概率分布更明显（比如你要对齐两个域的某一类的标签）[2], 减小域混淆[3]等等。

[1] Progressive Feature Alignment for Unsupervised Domain Adaptation
[2] Simultaneous Deep Transfer Across Domains and Tasks
[3] Minimum Class Confusion for Versatile Domain Adaptation
