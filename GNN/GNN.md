## 收集
[DeepGraphLibrary](https://www.dgl.ai/)

## 理论

### Spatial-based
[[Graph Attention Networks (GAT)]]
[[GIN (Graph Isomorphism Network)]]

### Spectral-based
[[Spectral Graph Theory]]
[[Graph Convolutional Networks (GCN)]]

## 定义
$$
G = (V, \mathbf{A}, \mathbf{X})
$$
$A$ is the adjacency matrix (assume binary)
$\mathbf{X} \in \mathbb{R}^{|V|\times m}$ is a matrix of node features

### 图的性质

[[Permutation invariant]]
Graph does not have a canonical order of the nodes.
Graph neural networks consist of multiple permutation equivariant / invariant functions.
## GNN Layer
*GNN Layer = Message + Aggregation*
### Message computation
**Message function** 
$$
m_u^{(l)} = \mathrm{MSG}^{(l)}(h_u^{(l - 1)})
$$
*example* Linear
$$
m_u^{(l)} = W^{(l)}h_u^{(l - 1)}
$$
### Message Aggregation
$$
h_v^{(l)} = \mathrm{AGG}^{(l)}\left(\{m_u^{(l)}\mid u \in N(v)\right)
$$
例如：$\mathrm{sum}(\cdot)$、$\mathrm{mean}(\cdot)$、$\mathrm{max}(\cdot)$
**Issue** Information from node $𝑣$ itself could get lost
修改**Aggregation**环节
$$
h_v^{(l)} = \mathrm{concat}\left(\mathrm{AGG}^{(l)}(\{m_u^{(l)}\mid u \in N(v)), m_v^{(l)}\right)
$$
### Nonlinearity (activation)
$\sigma(\cdot)$例如$\mathrm{ReLU}(\cdot),\mathrm{sigmoid}(\cdot)$

### 例子
#### [[Graph Convolutional Networks (GCN)]] 
$$
\begin{align} 
h_v^{(k + 1)} &= \sigma\left(W_k\sum_{u \in N(v)}\frac{h_u^{(k)}}{|N(v)|} + B_kh_v^{(k)}\right) \\
 &= \sigma\left(\sum_{u \in N(v)}W_k\frac{h_u^{(k)}}{|N(v)|} + B_kh_v^{(k)}\right)
\end{align}
$$
**Message**
$$
m_u^{(l)}=\frac{1}{|N(v)|}W^{(l)}h_u^{(l - 1)}
$$
**Aggregation**
$$
h_v^{(l)} = \sigma(\mathrm{sum}\left(\{m_u^{(l)}\mid u \in N(v)\}\right))
$$
#### [[GraphSAGE]]
$$
\begin{align} 
h_v^{(l)}  &= \sigma\left(W^{(l)}\cdot\mathrm{concat}(h_v^{(l-1)},\mathrm{AGG}(\{h_u^{(l-1)}\mid \forall u \in N(v\}))\right) \\
 &= \sigma\left(\mathrm{concat}(W^{(l)} h_v^{(l-1)},\mathrm{AGG}(\{ W^{(l)}h_u^{(l-1)}\mid \forall u \in N(v\}))\right)
\end{align}
$$
**Message**
$$
m_u^{(l)}=W^{(l)}h_u^{(l - 1)}
$$
**Aggregation**
$$
h_v^{(l)} = \sigma(\mathrm{concat}(m_v^{(l)},\mathrm{AGG}(\{ m_u^{(l)}\mid \forall u \in N(v\})))
$$
#### [[Graph Attention Networks (GAT)]]

### Layer in Practice
#### Linear
#### BatchNorm
使一批数据的均值在0，方差为1
#### Dropout
#### Actiation
#### Attention
#### Aggregation
