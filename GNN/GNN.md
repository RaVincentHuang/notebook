## 收集
[DeepGraphLibrary](https://www.dgl.ai/)

## 理论

### Spatial-based
[[GAT]]
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

### [[Aggregate Neighbors]]
Generate node embeddings based on local network neighborhoods.
Nodes aggregate information from their neighbors using neural networks.

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
[[Graph Convolutional Networks (GCN)]]