#artificial_intelligence #machine_learning
## Machine Learning
- An agent is learning if it improves its performance after making observations about the world.
	- When the agent is a computer, we call it machine learning: a computer observes some data, builds a <font color="#fac08f">model</font> based on the data, and uses the model as both a hypothesis about the world and a piece of software that can solve problems.
### 1. Supervised Learning
> The agent observes <font color="#fac08f">input-output(label) pairs</font> and learns a function that maps form input to output(label)
- Classification(discrete) vs. Regression(continuous)
- Function (hypothesis)
	- prior knowledge
	- <font color="#fac08f">Exploratory Data Analysis (EDA)</font>
		- visualizations
		- just try
	- For a Good Hypothesis
		- The true measure of a hypothesis is not how it does on the training set, but rather <font color="#fac08f">how well it handles inputs it has not yet seen (test set; not used in training procedure)</font>.
		- Bias(~underfitting) $\leftrightarrow$ Variance(~overfitting) : tradeoff
			- Ockhams's razor : "shave off" dubious explanations
	- How to find the Best Hypothesis : $$h^*=\text{argmax}_{h\in\mathcal{H}}P(h|data)$$
### 2. Unsupervised Learning
> The agent learns patterns in the input without any explicit feedback 
> clustering : detecting potentially useful clusters of input examples
- ##### Self-Supervised Learning
	- Strengths of SSL
		- Solving the pretext tasks allow the model to<font color="#fac08f"> learn good features</font>. 
		- We can automatically generate <font color="#fac08f">labels</font> for the pretext tasks. 
	- Implications of SSL
		- We usually don’t care about the performance of the self-supervised learning task, e.g., we don’t care if the model learns to predict image rotation perfectly. 
		- Evaluate the learned feature encoders on downstream target tasks.
### 3. Reinforcement Learning
> The agent learns from a series of reinforcements: rewards and pubishments (mainly in game)
![](https://i.imgur.com/hEcswab.jpeg)

## Basic Algorithms
- ### [[k-Nearest-Neighbors Classification]]
- ### [[k-Means Clustering]]
### Model Selection and Optimization
- #### I.I.D. Assumption (independent and identically distributed)
>"furture examples"
- #### Error Rate and Two Different Datasets (training/test)
>"optimal fit" : minimizes the error rate
- #### Hyperparameters and Three Datasets (training/validation/test)
    > hyperparameters : parameters of the model class, not of the individual model
	- K-fold cross-validation
		- The technique we can try if we don’t have enough data to make all three of these data sets.
		- First, we split the data into $k$ equal subsets. 
		- We then perform $k$ rounds of learning; on each round 1/$k$ of the data are held out as a validation set and the remaining examples are used as the training set.
		- Popular values for $k$ are 5 and 10.
		- Note that we still need a separate test set.
- #### Model selection : chooses a good hypothesis space
	-  Two Different Patterns That Occur![](https://i.imgur.com/niloCtF.jpeg)
	- code
```pseudo code
function MODEL-SELECTION(Learner,examples,k) returns a (hypothesis,error rate) pair
	err <- an array,indexed by size,storing validation-set error rates
	training_set,test_set <- a partition of examples into two sets
	for size 1 to ∞ do
		err[size] <- CROSS-VALIDATION(Learner,size,training_set,k)
		if err is starting to increase significantly then
			best_size <- the value of size with minimum err[size]
			h <- Learner(best_size,training_set)
			return h,ERROR-RATE(h,test_set) 

function CROSS-VALIDATION(Learner,size,example,k) returns error rate
	N <- the number of examples
	errs <- 0
	for i = 1 to k do
		validation_set <- examples[(i-1) x N/k:i x N/k]
		training_Set <- examples - validation_set
		h <- Learner(size,training_set)
		errs <- errs + ERROR-RATE(h,validation_set)
	return errs / k     //average error rate on validation sets,
						//accross k-fold cross-validation
```
- #### From Error Rates to Loss Functions (Regularization)
	- L1 loss (absolute-value loss) $$L_1(y,\hat{y})=|y-\hat{y}|$$
	- L2 loss (squared-error loss) $$L_2(y,\hat{y})=(y-\hat{y})^2$$
	- Generalizarion Loss (Logically)$$GenLoss_L(h)=\sum_{(x,y)\in\epsilon}P(x,y)L(y,h(x))$$
	- Empirical Loss (Practically)$$EmpLoss_{L,E}(h)=\sum_{(x,y)\in E}\frac{1}{N}L(y,h(x))$$
	- Four reasons why $\hat{h^*}$ May Differ from $f$
		- Unrealizability
		- Variance
		- Noise
		- Computational Complexity
	- Hyperparameter Tuning
		- Hand-tuning
		- Grid-search
		- Random search
		- Bayseain optimization
		- Population-based Training
 
- #### Optimization : finds the best hypothesis within that space