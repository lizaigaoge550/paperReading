##这篇文章讲了一些调优注意的事项
* initial learning rate
  * 一般初始化的值在10^-6 和 1之间，一般多层网路默认的初始化值0.01
* mini-batch size
  * 32是一个很好的默认值
  * number of hidden units
  * 一般所有层节点数相同或成金字塔状(第一层最多)
  * 第一层节点一般比输入要多,效果更好
  * 一些人增则化的时候仅仅惩罚W, 这确保了当正则化很强的时候, 预测的结果也会收敛到最优，而不是0
* Preprocessing
  * 数据先standardization
  * PCA
* Debuging
  * 当测试集的error很大，首要的问题是要看是否是由于在训练集的优化上很困难或者是由于过拟合,
    比较训练集和测试集
