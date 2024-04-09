$$
h_v^{(l)} = \sigma\left(W^{(l)}\mathrm{concat}(h_v^{(l-1)},\mathrm{AGG}(\{h_u^{(l-1)}\mid \forall u \in N(v\}))\right)
$$
事实上它是一个Two-stage aggregation的过程
+ **Stage 1**: Aggregate from node neighbors
$$
h_{N(v)}^{(l)} \gets \mathrm{AGG}(\{h_u^{(l-1)}\mid \forall u \in N(v\}))
$$
+ **Stage 2**: Further aggregate over the node itself