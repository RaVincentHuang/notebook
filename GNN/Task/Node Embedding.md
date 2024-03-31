## Graph Representation Learning
**Goal:** Efficient task-independent feature learning for machine learning with graphs!
**Task:** Map nodes into an embedding space
$$
\mathrm{ENC}: V \to \mathbb{R}^d
$$
### Components
**Encoder:** 
$$
\mathrm{ENC}(v) = \mathbf{z}_{v}
$$
**Similarity function:** specifies how the relationships in vector space map to the relationships in the original network
$$
\mathrm{simlarity}(u, v) \approx \mathbf{z}_{v}^{{\top}}\mathbf{z}_{u}
$$
#### Shallow Encoding
$$
\mathbf{Z} = \begin{pmatrix}
z_{v_{1}} z_{v_{2}}
\end{pmatrix}
$$

**DeepWalk**, **node2vec**
