## Graph Representation Learning
**Goal:** Efficient task-independent feature learning for machine learning with graphs!
**Task:** Map nodes into an embedding space
$$
\mathrm{ENC}: V \to \mathbb{R}^d
$$
### Components
#### Encoder 
$$
\mathrm{ENC}(v) = \mathbf{z}_{v}
$$

**Shallow Encoding**
$$
\begin{align}
\mathbf{Z}  & = \begin{pmatrix}
z_{v_{1}} &  z_{v_{2}} & \dots & z_{v_{n}}
\end{pmatrix} \in \mathbb{R}^{d \times n} \\
\mathrm{ENC}(v)  & = \mathbf{Z} \cdot v \quad \text{where}\  v \in \mathbb{I}^{n}
\end{align}
$$
#### Similarity function 
specifies how the relationships in vector space map to the relationships in the original network
$$
\mathrm{simlarity}(u, v) \approx \mathbf{z}_{v}^{{\top}}\mathbf{z}_{u}
$$
如何定义这种相似度呢？
+ linked
+ share neighbors
+ have similar “structural roles“
**DeepWalk**, **node2vec**

### Random Walk

**Def. ((Predicted) Probability)** 
$$
\Pr(v\mid \mathbf{z}_u)
$$
The (predicted) probability of visiting node $v$ on random walks starting from node $u$.

**neighbourhood**
$$
N_R(u) = \text{neighbourhood of $u$ obtained by some random walk strategy $R$}
$$
$$
\begin{align}
 & \arg \max_Z \sum_{u \in V} \log \Pr(N_R(u)\mid \mathbf{z}_u) \\
\text{Equivalently:}\quad  & \arg \min_Z \mathcal{L} = \sum_{u \in V}\sum_{v \in N_R(u)} -\log(\Pr(v\mid \mathbf{z}_u)) \\
\text{where}\quad  & \Pr(v\mid \mathbf{z}_u) = \mathrm{softmax}(\mathbf{z}_u) = \frac{\exp(\mathbf{z}_u^{\top}\mathbf{z}_v)}{\sum_{k\in V}\exp(\mathbf{z}_u^{\top}\mathbf{z}_n))}
\end{align}

$$
**时间复杂度**
$\mathcal{O}(|V|^2)$ ，可以用[[Negative smapling]]技术压缩
$$
-\log\left(\frac{\exp(\mathbf{z}_u^{\top}\mathbf{z}_v)}{\sum_{k\in V}\exp(\mathbf{z}_u^{\top}\mathbf{z}_n))}\right) \approx \log\left(\sigma(\mathbf{z}_u^{\top}\mathbf{z}_v))\right) + \sum_{i = 1}^k\log\left(\sigma(-\mathbf{z}_u^{\top}\mathbf{z}_{n_i}))\right), \quad n_i \thicksim P_V
$$
接下来采用[[Stochastic Gradient Descent (SGD)]]进行优化

**Strategies**
