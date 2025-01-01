#artificial_intelligence 
## Linear Functions 
- A different hypothesis space, one that has been used for hundreds of years 
	- The class of linear functions of continous-valued inputs.
	- We will cover linear regression with a univariate linear function, otherwise known as "fitting a straight line"
	- We will also cover the multivariate case, and how to turn linear function into classifiers by applying hard ans soft thresholds

### Univariate Linear Regression
- A univariate linear fumction (a straight line) with inpus $x$ and output $y$ has the form <font color="#d99694">$y = w_1x + w_0$</font>
	- $w_0, w_1$ are real-valued coefficients to be learned
	- **w** to be the vector $<w_0, w_1>$ $$h_w(x)=w_1x+w_0\qquad \text{or}\qquad h_w(x) = w^Tx\ \text{where }x=<1,x>$$
- The task of finding the $h_w$ that best fits the data is called <font color="#d99694">linear regression.</font>
	- To fit a line to the data, all we have to do is find the values of the weights $<w_0,w_1>$ that minimizes the empirical loss.
	- It is tradional to use the <font color="#d99694">squared-error loss function, $L_2$</font>, summed over all the training examples : $$Loss(h_w)=\sum_{j=1}^NL_2\Big(y_j,h_w(x_j)\Big)=\sum_{j=1}^NL_2\Big(y_j-h_w(x_j)\Big)^2=\sum_{j=1}^NL_2\Big(y_j-(w_1x_j+w_0)\Big)^2$$
- We would like to find <font color="#d99694">$w^*=argmin_wLoss(h_w)$</font>
	- The sum $\sum_{j=1}^N\Big(y_j-(w_1x_j+w_0)\Big)^2$ is minimized when its partial derivatives with respect to $w_0$ and $w_1$ are zero:$$\frac{\delta}{\delta w_0}\sum_{j=1}^N\Big(y_j-(w_1x_j+w_0)\Big)^2=0\qquad\text{and}\qquad\frac{\delta}{\delta w_1}\sum_{j=1}^N\Big(y_j-(w_1x_j+w_0)\Big)^2=0$$
	- $$\begin{align}w_1&=\frac{N(\sum_jx_jy_j)-(\sum_jx_j)(\sum_jy_j)}{N(\sum_jx_j^2)-(\sum_jx_j)^2}\\w_0&=\frac{\sum_jy_j-w_1(\sum_jx_j)}{N}\end{align}$$
	- ![|500](https://i.imgur.com/wvTz0nm.png)
	- ![|500](https://i.imgur.com/o5gmWfN.png)
### Weight Space
- Many forms of learning involve adjusting weights to minimize a loss, so it helps to have a mental picture of what's going on in <font color="#d99694">weight space</font> :
	- The space defined by all possible settings of the weights.
	- For univariate linear regression, the weight space defined by $w_0$ and $w_1$ is two dimensional, so we can graph the loss as a function of $w_0$ and $w_1$ in a 3D plot.
	- ![](https://i.imgur.com/hwjax5y.png)
	- We see that the loss function is <font color="#d99694">convex</font>; this is true for *every* linear regression problem with an $L_2$ loss function.
	- Convex functions gurantee a global optimum rather than local optima
- The univariate linear model vs. Complex model
	- Gradient Descent : A method for minimizing loss that does not depend on soling to find zeros of the derivarives, and can be applied to any loss function, no matter how complex.
	
### Gradient Descent![[Gradient Descent]]
### Multivariable Linear Regression
- Our hypothesis space is the set of functions of the form$$h_w(x_j)=w_0+w_1x_{j,1}+\cdots+w_nx_{j,n}=w_0+\sum_iw_ix_{j,i}$$
	- For a simpler notation, we can invent a dummy input attribute $x_{j,0}$, which is defined as always equal to 1
	- Then $h$ is simply the dot product of the weights and the input vector$$h_w(x_j)=w\cdot x_j=w^Tx=\sum_iw_ix_{j,i}$$
- The best vector of weights, $w*$, minimize squared-error loss over the examples$$w*=argmin_w\sum_jL_2(y_j,w\cdot x_j)$$
	- Gradient descent will reach the (unique) minimum of the loss function
		- $$w_i\leftarrow w_j+\alpha\sum_j\big(y_j-h_w(x_j)\big)\times x_{j,i}$$
	- With the tools of linear algebra and vector calculus, it is also possible to solve analytically for the $w$ that minimizes loss
		- Let $y$ be the vector of outputs for the traning examples, and $X$ be the data matrix, i.e., the matrix of inputs with one $n$-dimensional example per row.
		- Then the vector of predicted outputs is $\hat y=Xw$ and the squared-error loss over all the training data is $$L(w)=||\hat y-y||^2=||Xw-y||^2$$
		- ![](https://i.imgur.com/V747ut0.png)
- Regularization for Multivariable Linear Regression
	- With multivariable linear regression in high-dimensional spaces,
		- It is possible that some dimension that is actually irrelevant appears by chance to useful, resulting in overfitting
		- Thus, it is common to use <font color="#d99694">regularization</font> on multivariable linear functions to avoid overfitting
	- Recall that with regularization we minimize the total cost of a hypothesis, counting both the empirical loss and the complexity of the hypothesis$$Cost(h) = EmpLoss(h)+\lambda Complexity(h)$$
	- The complexity can be specified as a function of the weights$$Complexity(h_w)=L_q(w)=\sum_i|w_i|^q$$
		- With $q=1$, we have <font color="#d99694">$L_1$ regularization</font>, which minimizes the sum of the absolute values
		- With $q=2$, <font color="#d99694">$L_2$ regularization</font> minimizes the sum of squares
- Property of $L_1$ Regularization
	- $L_1$ regularization has an important advantage
		- It tends to produce <font color="#d99694">sparse model</font>
			- That is, if often sets many weights to zero, declaring the corresponding attributes to be completely irrelevant
	- ![](https://i.imgur.com/LSGADBz.png)
### ![[Linear Classification]]