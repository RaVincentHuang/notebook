## 收集
[DeepGraphLibrary](https://www.dgl.ai/)

## 理论

### Spatial-based
[[GAT]]
[[GIN (Graph Isomorphism Network)]]

### Spectral-based
[[Spectral Graph Theory]]
[[GCN]]

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

