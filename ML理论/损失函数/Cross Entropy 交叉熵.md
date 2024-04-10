考虑两个定义在相同的事件测度上的概率分布$p$和$q$，$p$相对与$q$的交叉熵表示为$q$对$p$编码时，事件集合中唯一标识一个事件所需要的平均比特数。
$$
H(p, q) := \mathrm{E}_p[-\log q] = H(p) + D_{\mathrm{KL}}(p||q)
$$
若$p$和$q$为离散分布
$$
H(p, q) = -\sum_{x\in \mathcal{X}}p(x)\log q(x)
$$