### Ref : 
- [Exact Inference in Bayesian Networks - GeeksforGeeks](https://www.geeksforgeeks.org/exact-inference-in-bayesian-networks/?ref=oin_asr1)
- [Approximate Inference in Bayesian Networks - GeeksforGeeks](https://www.geeksforgeeks.org/approximate-inference-in-bayesian-networks/?ref=gcse_outind)

## A Bayesian Network
> data structure to represent the dependencies among variables
> directed acylic graph (DAG) : no dircted cycles
> Each node $X_i$ has associated probability information $P(X_i|Parents(X_i))$ that quantifies the effect of the parents on the node

- CPT (Conditional Probability Table)

| B   | E   | P(A=true \| B,E) |
| --- | --- |:----------------:|
| t   | t   |       .95        |
| t   | f   |       .94        |
| f   | t   |       .29        |
| f   | f   |       .001       |

- Joint Distribution (based Chain rule)$$P(x_1,...,x_n)=\Pi_{i=1}^nP(x_i|Parents(X_i))$$

## Exact Inference
> Inferenc by Enumeration
> $$P(X|e) = \alpha P(X,e)=\alpha\sum_yP(X,e,y)$$

```pseudo code
function ENUMERATION-ASK(X,e,bn) returns a distribution over X
	inputs: X,the query variable
			e,observed values for variables vars
	Q(X) <- a distribution over X, initially empty
	for each value x[i] of X do
		Q(x[i]) <- ENUMERATE-ALL(vars,e[x[i]])
			where e[x[i]] is e extended with X = x[i]
	return NORMALIZE(Q(X))

function ENUMERATE-ALL(vars,e) returns a real number
	if EMPTY?(vars) then return 1.0
	V <- FIRST(vars)
	if V is an evidence variable with value v in e
		then return P(v|parents(V)) x ENUMERATE-ALL(RESR(vars),e)
		else return SUM_V{P(v|parents(V))} x ENUMERATE-ALL(REST(vars),e[v])
			where e[v] is e extended with V = v
```
- Performance : $O(2^n)$
## Approximate Inference
>Randomized sampling algorithms = Monte Carlo algorithms (<u>depends on the number of samplse generated</u>)
> Using $\hat{P}$ to mean an <font color="#fac08f">estimated</font> probability
- ### Direct Sampling
>The primitive element in any sampling algorithm<font color="#fac08f"> is the generation of samples</font> from a known probability distribution.

```pseudo code
function PRIOR-SAMPLE(bn) returns an event sampled from the prior specified by bn
	inputs: bn,a Bayesian network specifying joint distribution P(X[1],...,X[n])
	x <- an event with n elements
	for each variable X[i] in X[1],...,X[n] do
		x[i] <- a random sample from P(X[i]|parents(X[i]))
	return x
```
- ### Rejection Sampling
> Rejection sampling is a general method for producing samples from a hard-to-sample distribution given an easy-to-sample distribution.

- It can be used to compute conditional probabilities $P(X|e)$.
	- First, it generates samples from the prior distribution specified by the network.
	- Then, it <font color="#fac08f">rejects</font> all those that do not match the evidence ().
	- Finally, the estimate $\hat{P}(X=x|e)$ is obtained by counting how often $X=x$ occurs in the remaining samples. 
	- Let $\hat{P}(X|e)$ be the estimated distribution; it is computed by normalizing $N_{PS}(X,e)$, the vector of sample counts for each value of $X$ where the sample agree with the evidence $e$:$$\hat{P}(X|e)=\alpha N_{PS}(X,e)=\frac{N_{PS}(X,e)}{N_{PS}(e)}$$
	- From $P(x_1,...,x_n) \approx N_{PS}(x_1,...,x_m)/N$ , this becomes$$\hat{P}(X|e)\approx\frac{P(X,e)}{P(e)}=P(X|e)$$
```pseudo code
function REJECTION-SAMPLING(X,e,bn,N) returns an extimate of P(X|e)
	inputs: X,the query variable
			e,observed values for variable E
			bn,a Bayesian network
			N,the total number of samples to be generated
	local variables: C,a vector of counts for each value of X,initially zero
	for j = 1 to N do
		x <- PRIOR-SAMPLE(bn)
		if x is consistent with e then
			C[j] <- C[j]+1 where x[j] is the value of X in x
	return NORMALIZE(C)
```
- Challenges
	- Q: How many samples are required before we know that the resulting esimates are close to the correct answers with high probability?
		- A: The complexity of rejection sampling depends primarily on<font color="#fac08f"> the fraction of samples that are accepted</font>.
			- This fraction is exactly equal to the prior probability of the evidence 
	- Unfortunately, for complex problems with many evidence variables, <font color="#fac08f">this fraction is vanishingly small</font>.
### Importance Sampling
>Importance sampling aims to emulate the effect of sampling from a distribution $P$ using samples from another distribution $Q$.
>$$\hat{P}(z|e)=\frac{N_Q(z)}{N}\cdot\frac{P(z|e)}{Q(z)}\approx Q(z)\frac{P(z|e)}{Q(z)}=P(z|e)$$

- As for which $Q$ to use, we want one that is <font color="#fac08f">easy to sample from and as close as possible to the true posterior $P(z|e)$</font>.
	- The most common approach is <font color="#fac08f">likelihood weighting</font>.
### Likelihood Weighting
>The algorithm <font color="#fac08f">fixes</font> the values for the evidence variables $E$ and <font color="#fac08f">samples</font> all the nonevidence variables in topological order, each conditioned on its parents.

$$Q_{WS}(z)=\Pi_{i=1}^lP(z_i|parents(Z_i)),\quad Z\ \text{is non-evidence}$$
$$\begin{align}w(z)&=\frac{P(z|e)}{Q_{WS}(z)}=\alpha\frac{P(z,e)}{Q_{WS}(z)} =\alpha\frac{\Pi_{i=1}^lP(z_i|parents(Z_i))\Pi_{i=1}^mP(e_i|parents(E_i))}{\Pi_{i=1}^lP(z_i|parents(Z_i))}\\&=\alpha\Pi_{i=1}^mP(e_i|parents(E_i))\end{align}$$
```pseudo code
function LIKELIHOOD-WEIGHTING(X,e,bn,N) returns an estimate of P(X|e)
	inputs :X,the query variable
			e,observed values for variables E
			bn,a Bayesian network specifying joint distribution P(X[1],...,X[n])
			N,the total number of samples to be generated
	local variables: W,a vector of weighted counts for each value of X,imitially 0
	for j = 1 to N do
		x,w <- WEIGHTED-SAMPLE(bn,e)
		W[j] <- W[j]+w where x[j] is the value of X in x
	return NORMALIZE(N)

function WEIGHTED-SAMPLE(bn,e) returns an event and a weight
	w <- 1; x <- an event with n elements, with values fixed from e
	for i = 1 to N do
		if X[i] is an evidence variable with values x[i][j] in e
			then w <- w x P(X[i] = x[i][j]|parents(X[i]))
			else x[i] <- a random sample from P(X[i]|parents(X[i]))
	return x,w		
```
- Pros and Cons
	- Because likelihood weighting uses all the samples generated, it can be much more efficient than rejection sampling.
	- It will, however, suffer a degradation in performance as the number of evidence variables increases.
		- This is because most samples will have <font color="#fac08f">very low weights</font> and hence the weighted estimate will be dominated by the tiny fraction of samples that accord more than an infinitesimal likelihood to the evidence.