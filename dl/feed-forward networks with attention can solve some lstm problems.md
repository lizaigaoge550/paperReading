
主要是把lstm的每个cell的输出 ![](http://latex.codecogs.com/gif.latex?h_t) 

![iamge](lstm_cell.png)

![](http://latex.codecogs.com/gif.latex?i_t = \\sigma(W_i[h_{t-1},x_t]+b_i))

![](http://latex.codecogs.com/gif.latex?f_t = \\sigma(W_f[h_{t-1},x_t]+b_f))

![](http://latex.codecogs.com/gif.latex?\\widetilde{c_t} = \\tanh(W_c[h_{t-1},x_t])+b_c)

![](http://latex.codecogs.com/gif.latex?c_t = f_t*c_{t-1}+i_t*\\widetilde{c_t})

![](http://latex.codecogs.com/gif.latex?o_t = \\sigma(W_o[h_{t-1},x_t]+b_o))

![](http://latex.codecogs.com/gif.latex?h_t = o_t*\\tanh(c_t))

![](http://latex.codecogs.com/gif.latex?i_t = c_t) 的解释是我们遗忘后的值加上添加后的值 ![](http://latex.codecogs.com/gif.latex?f_t)

是 ![](http://latex.codecogs.com/gif.latex?i_t = \\sigma) 函数, 值在[0-1]之间. 所以![](http://latex.codecogs.com/gif.latex?i_t = f_t*c_{t-1})

就代表遗忘后剩余的值, ![](http://latex.codecogs.com/gif.latex?i_t) 描述了哪些值我们需要更新的.tanh值在[-1,1]之间代表创造出一个新的候选向量，可能会添加

到这个状态。 sigmoid layer值在[0-1]之间描述了每一个组件值有多少可以通过.

这篇文章中在输出层![](http://latex.codecogs.com/gif.latex?h_t)上做了些改动
![](http://latex.codecogs.com/gif.latex?a(h_t) = tanh(W_{hc}h_t+b_{hc}))
假设 ![](http://latex.codecogs.com/gif.latex?h_t) 是 20\*200 的矩阵, ![](http://latex.codecogs.com/gif.latex?W_{hc})是 1\*20 的矩阵, 
![](http://latex.codecogs.com/gif.latex?b_{hc}) 是 1\*1 ![](http://latex.codecogs.com/gif.latex?a(h_t))是一个1\*200的矩阵

然后 ![](http://latex.codecogs.com/gif.latex?e_t=a(h_t))

![](http://latex.codecogs.com/gif.latex?\\alpha_{t} = \\frac{exp(e_t)}{\\sum_{k=1}^{T}exp(e_k)}),

![](http://latex.codecogs.com/gif.latex?c=\\sum_{t=1}^{T}\\alpha_t h_t)

![](http://latex.codecogs.com/gif.latex?\\alpha_t) 是一个1\*200的矩阵 , ![](http://latex.codecogs.com/gif.latex?h_t)是一个20\*200的矩阵

所以c是一个20\*200的矩阵, 再加一个MLP层, ![](http://latex.codecogs.com/gif.latex?s = ReLU(W_{cs}c+b_{cs})), 假设是 200\*200 然后一个softmax层, 

200*class_num, 损失函数为tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits(pred,y))

论文地址 http://pan.baidu.com/s/1o7L0HHS 1.pdf






