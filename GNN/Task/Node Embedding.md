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
