#artificial_intelligence  #probability #machine_learning
## Decision Trees
- A ***decision tree*** is a representation of a function that maps a vector of attribute values to a single output value a <font color="#e36c09">"decision"</font>
	- A decision tree reaches its decision by **performing a sequence of tests**, starting at the root and following the appropriate branch until a leaf is reached.
	- Each internal node in the tree corresponds to a test of the value of one of the input attributes, the branches from the node are labeled with the possible values of the attribute, and the leaf nodes specify what value is to be returned by the function.
- In general, the input and output values can be discrete or continuous
- Notation
	- We will use $j$ to index the examples ($x_j$ is the input vector for the $j$th example and $y_j$ is the output), and $x_{j,i}$ for the $i$th attribute of the $j$th example.
- ![](https://i.imgur.com/mHvHEFu.png)
- We want to find a decision tree that is consistent with the training data and is as small as possible
	- With simple heurisitcs, we can efficiently find one that is close to the smallest
### Learn-decision-tree algorithm 
- Greedy divide-and-conquer strategy 
	- Always test the most important attribute first, then recursively solve the smaller subproblems that are defined by the possible results of the test. 
	- By <font color="#e36c09">“most important attribute”</font>, we mean the one that makes the most difference to the classification of an example. 
	- That way, we hope to get to the correct classification with a small number of tests, meaning that all paths in the tree will be short and the tree as a whole will be shallow. 
- four cases to consider for these recursive subproblems :
	1. END : If the remaining examples are **all positive(negative)** then we are done
	2. GENERAL : If there are **some positive and some negative examples**, then **choose the best attribute to split them**. 
	3. No Examples left : We return the most common output value
	4. No Attributes left : 
		- It means that these examples have exactly the same description, but different classifications.
			- **Error** or <font color="#e36c09">Noise</font> in the data.
		- Return **the most common output**
```pseudo
function LEARN-DECISION-TREE(examples, attributes, parent_examples) returns a tree
1	if examples is empty then return PLURALITY-VALUE(parent_examples)
2	else if all examples have the same classification then return the classification
3	else if attributes is empty then return PLURALITY-VALUE(examples)
4	else
5		A <- argmax_{a in attributes} IMPORTANCE(a,examples)
6		tree <- a new decision tree with root test A
7		for each value v of A do
8			exs <- {e : e in examplse and e.A = v}
9			subtree <- LEARN-DECISION-TREE(exs, attributes-A, examples)
10			add a branch to _tree_with label (A = v) and subtree _subtree_
11		return tree
```

### Choosing Attribute Tests
- Using the notion of information gain, which is defined in terms of [[Entropy]]
- If a training set contains $p$ positive examplse and $n$ negative examples, then the entropy of the output variables on the whole set is  $$H(output) = B(\frac{p}{p+n})$$
- The result of a test on an attribute $A$ will give us some information, thus reducing the overall entropy by some amount
	- We can measure this reduction by looking at the entropy remaining after the attribute test.
	- An attribute $A$ with $d$ distinct values divides the training set $E$ into subsets $E_1,\cdots,E_d$ -> $B(\frac{p_k}{p_k+n_k})$
- $$\begin{align}Remainder(A)&=\mathbb{E}_{E_k,k=1,\cdots,d}[H(E_k)]=\sum_{k=1}^d\frac{p_k+n_K}{p+n}B(\frac{p_k}{p_k+n_k})\\ Gain(A)&=B(\frac{p}{p+n}) - Remainder(A)\end{align}$$
	- The information gain, $Gain(A)$ is just what we need to implement the IMPORTANCE function 