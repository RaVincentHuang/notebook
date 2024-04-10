$$
h_v^{(l)} = \sigma\left(\sum_{u\in N(v)}\alpha_{v, u}W^{(l)}h_u^{(l - 1)}\right)
$$
事实上，注意力参数$\alpha_{v, u}$可以学习产生。

$$
\begin{align}
e_{v, u}  & = a(W^{(l)}h_{u}^{(l - 1)}, W^{(l)}h_v^{(l - 1)}) \\
a_{v, u}  & = \mathrm{softmax}(e_{v, u})
\end{align}
$$
首先通过一个注意力层计算二者的权重，然后使用[[Softmax]]进行归一化。

对于注意力层的设计，下面给一个例子
$$
e_{u, v} = \mathrm{Linear}(\mathrm{concat}(W^{(l)}h_{u}^{(l - 1)}, W^{(l)}h_v^{(l - 1)}))
$$
使用单层线性层作为权重。

## 多头注意力
多头注意力的思路在于分出多个注意力通道。
$$
\begin{align}
h_v^{(l), 1} = \sigma\left(\sum_{u\in N(v)}\alpha_{v, u}^1W^{(l)}h_u^{(l - 1)}\right) \\
h_v^{(l), 2} = \sigma\left(\sum_{u\in N(v)}\alpha_{v, u}^2W^{(l)}h_u^{(l - 1)}\right) \\
h_v^{(l), 3} = \sigma\left(\sum_{u\in N(v)}\alpha_{v, u}^3W^{(l)}h_u^{(l - 1)}\right)
\end{align}
$$
最后将它们聚合起来
$$
h^{(l)}_v = \mathrm{AGG}(h_v^{(l), 1}, h_v^{(l), 2}, h_v^{(l), 3})
$$

Allows for (implicitly) specifying different importance values ($\alpha_{v, u}$) to different neighbors.