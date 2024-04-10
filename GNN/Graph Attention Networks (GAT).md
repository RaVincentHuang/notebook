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