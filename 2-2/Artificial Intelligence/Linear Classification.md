## Linear Classification
- Linear functions can be used to do classification as well as regression
	- Ex : earthquake / nuclear explosion classification
	- ![](https://i.imgur.com/RRoh82i.png)
- Decision Boundary 
	- line (or a surface, in higher dimensions) that separates the two classes
	- Called a <font color="#fac08f">linear separator</font> and data that admit such as a seperator are called <font color="#fac08f">linearly separable</font>
## Perceptron Learning Rule
- Linear classifiers with a Threshold Function$$h_w(x)=Threshold(w\cdot x)\ \text{where }Threshold(z)=1\ \text{if }z\geq0\ \text{and }0\ \text{otherwise}$$
	- ![|200](https://i.imgur.com/S3y1uhL.png)
	- Problem : Here we can't utilize both (1) gradient descent and (2) computation in closed form to derive the optimal weights ($w^*$)
		- Because the gradient is zero almost everywhere in weight space except at those points where $w\cdot x = 0$, and at those points the gradient is undefined
- Perceptron Learning Rule
	- For a single example $(x,y)$, we have $$w_i\leftarrow w_i+\alpha(y-h_w(x))\times x_i$$ <font color="#d99694">which is essentially identical to the update rule for linear regression</font>
	- Both the true value $y$ and the hypothesis output $h_w(x)$ are either 0 or 1, so there are three posibilites 
		1. If the output is correct then the weights are not changed
		2. If $y$ is 1 but $h_w(x)$ is 0, then $w_i$ is <font color="#d99694">increased</font> when the corresponding input $x_i$ is positive and <font color="#d99694">decreased</font> when $x_i$ is negative. This make sense, because we want to make $w\cdot x$ bigger so that $h_w(x)$ output as 1
		3. If $y$ is 0 but $h_w(x)$ is 1, then $w_i$ is <font color="#d99694">decreased</font> when the corresponding input $x_i$ is positive and <font color="#d99694">increased</font> when $x_i$ is negative. This make sense, because we want to make $w\cdot x$ smaller so that $h_w(x)$ output as 0
- Typically, the learning rule is applied one example at a time, choosing examples at random (as in stochastic gradient descent)
- ![](https://i.imgur.com/f1q0Sgc.png)

## Linear Classification with Logistic Regression 
- Problems of Linear Classification with a Hard Threshold
	- The hypothesis $h_w(x)$ it **not differentiable** and is a discontinous function of its inputs and its weights. This makes learning with the perceptron rule a very unpredictable adventure
	- Furthermore, the linear classifier always announces a complexity confident prediction of 1 or 0, even for examples that are very close to the boundary; it would be better if it could classify some examples as a clear 0 or 1, and others as unclear borderline cases
	- Sol : <font color="#d99694">"softening the treshold functions"</font>
- Logistic Function (sigmoid function)
	- ![|300](https://i.imgur.com/1PR0nuW.png)
	- With the logistic function replacing the threshold function, we have$$h_w(x)=Logistic(w\cdot x)=\frac{1}{1+e^{-w\cdot x}}$$
	- The process of fitting the weights of this model to minimize loss on a data set is called <font color="#d99694">logistic regression</font>
- How to Compute $w*$ in Logistic Regression
	- using L2 loss function ($g$ to stand for the logistic function)
		- hypotheses no longer output just 0 or 1, its derivative
		- ![](https://i.imgur.com/O0YuXFO.png)
		- The derivative $g'$ of the logistic function satisfies <font color="#d99694">$g'(z)=g(z)(1-g(z))$</font>
			- ![](https://i.imgur.com/fE3elJm.png)
		- The weight update for minimizing the loss take a step in the direction of the difference betwwen input and prediction, $(y-h_w(x))$, and the length of that step depends on the constant $\alpha$ and $g'$$$w_i\leftarrow w_i+\alpha(y-h_w(x))\times h_w(x)(1-h_w(x))\times x_i$$
