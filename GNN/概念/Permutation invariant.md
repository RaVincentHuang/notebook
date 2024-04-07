图有置换不变性
图在同构意义下是等价的

对于一个图的嵌入映射
$$
f: \mathcal{G} \to \mathbb{R}^d
$$
若对于任意的图同构
$$
\sigma: \mathcal{G} \to \mathcal{G}
$$
和同构对应的置换矩阵$\mathbf{P}_\sigma$，使得有
$$
f(G,\mathbf{X}) = f(\sigma(G), \mathbf{P}_\sigma\mathbf{X})
$$
那么$f$保持了图的置换不变性
$𝑓$ is a permutation invariant function.

进一步的，若我们仅考虑图的节点信息，得到下面的定义
**Definition** For any graph function $𝑓: \mathbb{R}^{|V|\times |V|} \times\mathbb{R}^{|V|\times m} \to \mathbb{R}^d$ $𝑓$ is permutation invariant if 
$$

$$
