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
#### [[BatchNorm]]
使一批数据的均值在0，方差为1
**Input** $X \in \mathbb{R}^{N\times D}$: $N$ node embedding。
**Parameters** $\gamma, \beta \in \mathbb{R}^{D}$
**Output** $Y \in \mathbb{R}^{N\times D}$ Normalized node embeddings
$$
\begin{align}
\mu_j  & = \frac{1}{N}\sum_{i = 1}^N X_{i, j} \\
\sigma_j^2  & = \frac{1}{N}\sum_{i = 1}^N (X_{i, j} - \mu_j)^2 \\
 \hat{X}_{i,j}  & = \frac{X_{i,j} - \mu_j}{\sqrt{\sigma_j^2 + \epsilon}}  \\
Y_{i, j}  & =\gamma \hat{X}_{i,j} + \beta_j
\end{align}
$$
*为什么这里要加一个额外的线性层？*
#### [[Dropout]]
减少过拟合：训练时以概率$p$随机移除某些神经元。
**GNN**中Dropout is applied to the *linear layer* in the message function.
#### Actiation
[[Rectified linear unit (ReLU)]]
[[Sigmoid]]
[[Parametric ReLU]]
#### Attention
[[Graph Attention Networks (GAT)]]
#### Aggregation


## Layers Connectivity
**over-smoothing problem**: all the node embeddings converge to the same value.
 + he embedding of a node is determined by **its** receptive field
 + If two nodes have highly-overlapped receptive fields, then **their embeddings are highly similar**
### 减少层数
**GNN**的层数不宜过多，层数略高于需求感受野的大小。
+ make aggregation / transformation become a deep neural network!
+ Add layers that do not pass messages
	E.g., we can add MLP layers (applied to each node) before and after
GNN layers, as **pre-process layers** and **post-process layers**

**Pre-processing layers** Important whenencoding node features is necessary.
	E.g., when nodes represent images/text
**Post-processing layers**: Important when reasoning / transformation over node
embeddings are needed
	E.g., graph classification, knowledge graphs

### 残差连接
Node embeddings in earlier GNN layers can sometimes better differentiate nodes.

$$
\mathcal{F}(\mathbf{x}) \to \mathcal{F}(\mathbf{x}) + \mathbf{x}
$$
[[ResNet]]
![[Pasted image 20240410171408.png]]
$$
h_v^{(k + 1)} = \sigma\left(W_k\sum_{u \in N(v)}\frac{h_u^{(k)}}{|N(v)|} + B_kh_v^{(k)}\right)
$$
$$
h_v^{(k + 1)} = \sigma\left(W_k\sum_{u \in N(v)}\frac{h_u^{(k)}}{|N(v)|} + B_kh_v^{(k)} + h_v^{(k)}\right)
$$
**Directly skip to the last layer**
$$
h_v^{final} = \mathrm{AGG}\left(\left\{h_v^{(l)}\right\}_{l = 1}^L\right)
$$
![[Pasted image 20240410171430.png]]

## Manipulate Graphs
Raw input graph $\ne$ computational graph
+ **Feature level** The input graph *lacks features* $\to$ **feature augmentation**
+ **Structure level** 
	+ The graph is too sparse $\to$ inefficient message passing $\to$ Add virtual nodes / edges
	+ The graph is too dense $\to$ message passing is too costly $\to$ Sample neighbors when doing message passing
	+ The graph is too large $\to$ cannot fit the computational graph into a GPU $\to$ Sample subgraphs to compute embeddings

### Feature Augmentation
+ Input graph does not have node features

![[Pasted image 20240410171128.png]]
+ Certain structures are hard to learn by GNN
	+ Clustering coefficient
	+ PageRank
	+ Centrality


### Add Virtual Nodes / Edges
*Augment sparse graphs*
**Edge** 使用二步的邻接矩阵$A + A^2$代替$A$
**Node** 加入一个连接所有节点的虚拟节点
	Greatly improves **message passing** in sparse graphs
### Node Neighborhood Sampling
**Dense/large graphs, high-degree nodes**: *(Randomly) determine a node’s neighborhood for message passing*
*需要理论保证*

## 训练
### Prediction Heads
*Different task levels require different prediction heads*
#### Node-level prediction
After GNN computation, we have 𝑑-dim node embeddings $\{h_v^{(L)} \in \mathbb{R} \mid \forall v \in G\}$
	*𝑘-way prediction*
$$
\hat{y}_v = \mathrm{Head}_{\mathrm{node}}(h_v^{(L)}) = W^{(H)}h_v^{(L)}
$$
where $W^{(H)} \in \mathbb{R}^{k\times d}$ is a mapping that$: \mathbb{R}^d \to \mathbb{R}^k$ so that $\hat{y}_v \in \mathbb{R}^k$

