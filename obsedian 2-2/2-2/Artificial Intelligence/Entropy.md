#probability #artificial_intelligence #information_theory 
## Entropy
- <font color="#fac08f">(Self-)Information</font> of an event $X = x$
	$$I(x)=-\log{P(x)}$$
	- Base : $e$, $2$ (bits, shannons)
	- deals only with a single outcome
- (shannon) Entropy :$$H(x)=\mathbb{E}_{x~P(X)}[I(x)]=-\mathbb{E}_{x~P(x)}[\log P(x)]$$
- Kullback-Leibler (KL) Dibergence : $$D_{KL}(P||Q)=\mathbb{E}_{x~P(x)}[\log\frac{P(x)}{Q(x)}]=\mathbb{E}_{x~P(x)}[\log P(x) -\log Q(x)]$$
	- It can measure how different these two distributions
	- The KL divergence is **non-negative**.
	- **The KL divergence is 0** if and only if 𝑃 and 𝑄 are the same distribution.
	- It is often conceptualized as measuring some sort of distance between these distributions. However,<font color="#fac08f"> it is not a true distance measure</font> because it is not symmetric: 
		- $𝐷_{𝐾𝐿}$ (𝑃 ∥ 𝑄) ≠ $𝐷_{𝐾𝐿}$ (𝑄 ∥ 𝑃) for some 𝑃 and 𝑄.
- Cross-Entropy :$H(P,Q)=H(P)+D_{KL}(P||Q)$$$H(P,Q)=-\mathbb{E}_{x~P(x)}\log Q(X)$$