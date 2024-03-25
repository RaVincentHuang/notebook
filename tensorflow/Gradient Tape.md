TF2自动求导通过自动求导记录器(Gradient Tape)实现。具体分两步：
1. 通过定义一个tf.GradientTape() 上下文，监控在其中的一系列操作的依赖关系。实际上就是如前所述，根据系列操作的依赖关系， 推导出其中监控变量的梯度求解依赖关系图计算图。;
2. 之后调用 tape.gradient 根据背后推导出的 梯度求解计算图来计算梯度。

**对于变量的梯度**

```python
import tensorflow as tf 
x = tf.Variable (initial_value =2.)
with tf.GradientTape () as tape : # 在 tf .GradientTape () 的上下文内，所有计算步骤都会被记录以用于求导
	y = tf.square (x)
	y_grad = tape.gradient (y, x) # 计算y关于x的导数
	print (y, y_grad)
	#运 行 结 果 如 下：
’’’
tf.Tensor(4.0, shape=(), dtype=float32 ) 
tf.Tensor(4.0, shape=(), dtype=float32 )
	’’’
```
**对于常量的梯度**
```python
x = tf . ones ((2,2) )

with tf . GradientTape () as tape :
	tape .watch(x) # x为constant， 必 须 显 式 监 控
	y = tf . reduce_sum(x) 6 z = tf . multiply (y,y) 7 8 dz_dx = tape . gradient ( z , x)
```