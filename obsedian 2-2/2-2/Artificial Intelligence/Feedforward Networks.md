#artificial_intelligence #deep_learning #neural_networks 
## Feedforward Networks
- A (deep) <font color="#b7dde8">feedforward (neural) network</font>, or called <font color="#b7dde8">multi-layer perceptrons (MLPs)</font> has **connections only in one direction**
	- It forms a **directed acyclic graph** with designated input and output nodes.
	- Each node computes a function of its inputs and passes the result to its successors in the network
	- Information flows through the network from the input nodes to the output nodes, and there are no loops.
- Vs. <font color="#b7dde8">recuurent netwroks</font> ![](https://i.imgur.com/ozQNcBe.png)
- In neural networks, input values are typically continuous, and nodes take continuous inputs and produce continuoys outputs
	- Some of the inputs to nodes are parameters of the network
	- The network learns by adjusting the values of these parameters so that the network as a whole fits the training data.
- The goal of a feedforward network is to approximate some function $f^*$
	- A feedforward network defines a mapping $y=f(x;\theta)$ and learns the value of the parameter $\theta$ that result in the best function approximation
- Feedforward networks are called <font color="#b7dde8">networks</font> because they are typically represented by composing together many different functions
## Definition
- Depth : The overall length of the chain (\# of hidden layers)
	- Hidden layers : the layer between the input and output layer
		- typically vector-valued
		- consisting of many units that act in *parallel*, each representing a vector-to-scalar function.
	- Output layers : final layer of a feedforward network
- Width : The dimensionality of these hidden layers
- ![](https://i.imgur.com/wCe0gR3.png)
- Each node within a network is called a <font color="#b7dde8">unit</font> (or <font color="#b7dde8">perceptron</font>)
## Computation of Feedforward Networks
1. calculates the weighted sum($w_{i,j}a_i$) of the inputs from predecessor nodes($in_j$)
2. applies a nonlinear function($g_j$) to produce its output
$$\begin{align}a_j &= g_j\bigg(\sum_iw_{i,j}a_i\bigg)\equiv g_j(in_j)\\&=g_j(w^Tx)\end{align}$$
![](https://i.imgur.com/OyfkwLJ.png)
- Activation Functions (<font color="#d99694">nonlinear</font> is important)
	- If it were not nonlinear, any composition of units would still represent a linear function (meaning of depth $\downarrow$)
	- <font color="#d99694">universal approximation theorem</font>
		- a network with just two layers of computational units, the first nonlinear and the second linear, can approximate any continuous function to an arbitrary degree of accuracy.
	- Variety functions that are used.
		- The logistic or sigmoid function$$\sigma(x)=1/(1+e^{-x})$$
		- The ReLU function (Rectified Linear Unit)$$max(0,x)$$
		- The softplus function, a smooth version of the ReLU function
		- The tanh function$$tanh(x)=\frac{e^{2x}-1}{e^{2x}+1}$$
		- ![](https://i.imgur.com/oluYzuN.png)
## Computation of Feedfoward Networks with Another Notation
- ![](https://i.imgur.com/sR5JvBv.png)
- We first construct $M$ linear combinations of the input variable $x_1,\cdots,x_D$ in the form$$a_j=\sum_{i=1}^Dw_{ji}^{(1)}x_i+w_{j0}^{(1)}$$
	- where $j=1,\cdots,M$, and the superscript (1) indicates that the corresponding parameters are in the first *layer* of the network
		- We refer to the parameters $w_{ji}^{(1)}$ as <font color="#e5b9b7">weights</font> and the parameters $w_{j0}^{(1)}$ as <font color="#e5b9b7">biases</font>
		- The quantities $a_j$ are known as <font color="#e5b9b7">activations</font>
		- Each of the activations is transformed using a *differentiable, nonlinear* <font color="#e5b9b7">activation function</font> $h(\cdot)$ to give$$z_j=h(a_j)$$
		- $z_j$ are called <font color="#e5b9b7">hidden units</font>
- These values $(z_i)$ are again linearly combined to give <font color="#e5b9b7">output unit activations</font>$$a_k=\sum_{j=1}MDw_{kj}^{(2)}z_j+w_{k0}^{(2)}$$
	- where $k=1,\cdots,K$, and $K$ is the total number of outputs
		- This transformation corresponds to the second layer of the network
		- Finally, $a_k$ are transformed using an <u>appropriate activation function</u> to give a set of network outputs $y_k$
			- For standard regression problems, the activation function is the **identity** $(y_k=a_k)$
			- For multiple binary classification problems, we use a **logistic sigmoid** function so that $y_k=\sigma(a_k)$, where$$\sigma(a)=\frac{1}{1+e^{-a}}$$
			- For multiclass problems, a <font color="#e5b9b7">softmax</font> activation function of the form$$\frac{exp(a_k)}{\sum_jexp(a_j)}$$
- We can combile these various stages to give the overall network function that, for sigmoid output unit act. functions, take the form$$y_k(x,w)=\sigma\Bigg(\sum_{j=1}^Mw_{kj}^{(2)}h\bigg(\sum_{j=1}^Dw_{ji}^{(1)}x_i+w_{j0}^{(1)}\bigg)+w_{k0}^{(2)}\Bigg)$$
	- where the set of all weight and bias parameters have been grouped together into a vector **w**
	- This process can be interpreted as a <font color="#e5b9b7">forward propagation</font> of information
	- Thus, the neural network model is simply a nonlinear function from a set of input variables **x=$\{x_i\}$** to a set of output variables $\{y_k\}$ controlled by a vector **w** of adjustable parameters
	- Note that the digaram does not represent probabilistic graphical models such as Bayesian networks, because the internal nodes represent deterministic variables rather than stochastic ones.
- Simplification of the equations
	- The bias parameters can be absorbed into the set of weight parameters by defining an additional input variable $x_0$ whose value is clamped at $x_0=1$$$a_j=\sum_{i=0}^Dw_{ji}^{(1)}x_i$$
	- We can similarly absorb the second-layer biases, so that the overall network function becomes$$y_k(x,w)=\sigma\Bigg(\sum_{j=0}^Mw_{kj}^{(2)}h\bigg(\sum_{i=0}^Dw_{ji}^{(1)}x_i\bigg)\Bigg)$$
	- Furthermore, we can utlize vectors to further simplify the equation $$y(x,w)=\sigma\big(W^{(2)}h(W^{(1)}x)\big)$$
	- Feedforward network are typically <font color="#e5b9b7"><u>fully-connected</u></font>
- How to Count the Number of Layers in NNs
	- ![|300](https://i.imgur.com/8caakzv.png)
		- This network may be described as a **3-layer networks**
			- which counts the number of layer of units, and treats the inputs as units
		- Sometimes, it is described as a **single-hidden-layer network**
			- which counts the number of layers of hidden units.
		- This can also be called as a **two-layer network**
			- it is the number of layers of adaptive weights that is important for determining the network properties