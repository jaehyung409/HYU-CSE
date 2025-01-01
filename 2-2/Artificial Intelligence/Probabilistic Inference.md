#probability #artificial_intelligence 
## Full Joint Distribution
> "knowledge base" from which <font color="#fac08f">answers to all questions may be derivd</font>
- Marginalization
- Conditioning
- Conditional Probabilities
- Normalization
	> We can calculate $P(A|B)$ even if we don't know the value of $P(B)$
	> $P(A|B)=\alpha P(A,B)$
- General inference rule$$P(X|e)=\alpha P(X,e)=\alpha\sum_yP(X,e,y)$$
	- $\alpha = \frac{1}{P(e)}$
	- $y$ = ignore(remaining unobserved variables)
- size : $O(2^n)$
	- factorize with (chain rule, independence, conditional independence)
	- A Bayesian network

## [[A Bayesian Network]]