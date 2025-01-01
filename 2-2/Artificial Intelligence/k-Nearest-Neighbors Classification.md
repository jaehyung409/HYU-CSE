#artificial_intelligence #machine_learning #algorithms 
## Classify : Supervised Learning -> Classification

## k-Nearest-Neighbors Classification
- Expansion of Nearest-Neighbors Classification
> Algorithm that, given an input, chooses the most common class out of the k nearest data points to that input
> ![](https://i.imgur.com/nvKmUlU.jpeg)

- Non-parametric method for both classification and regression.
- Strengths
	- (Nearly) no traning is required (non-parametric)
- Weaknesses
	- A drawback of the basic “majority voting” classification occurs when the class distribution is **skewed**.
		- That is, examples of a more frequent class tend to dominate the prediction of the new example, because they tend to be common among the nearest neighbors due to their large number.
		- One way to overcome this problem is to weight the classification, taking into account the distance from the test point to each of its nearest neighbors. (weighted nearest neighbors)
	- **Parameter selection**: the best choice of depends upon the data; a good should be selected by various heuristic techniques.
