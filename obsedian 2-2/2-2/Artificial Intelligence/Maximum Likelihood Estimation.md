## Maximum Likelihood Estimation (MLE)
- Suppose that for a problem, we have a set of examplse $\{x_n\}_{n=1}^N$ that are drawn independently from a true but unknown distribution $P_{data}(x)$
- Then we try to model that true distribution by a parametric model $P_{model}(x;w)$ with $w$ (or $\theta$) as the parameters
- To get the best model, we need to find such $w$ that yields the most similar outcome of $P_{model}(x;w)$ to $P_{data}(x)$ (strictly, $P_{training}(x;w)$)
- We can use MLE principle to find such $w$, which is defined as$$w_{ML}=argmax_wP_{model}(x;w)$$
- Since $x_n$ are independent of each other(IID assumption), then we can write $w_{ML}$ as![](https://i.imgur.com/3uzULYp.png)
- By taking the loarithm of the quantity for computation stability,![](https://i.imgur.com/abskbqh.png)
