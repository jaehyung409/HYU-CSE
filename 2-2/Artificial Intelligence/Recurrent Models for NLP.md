## Recurrent Models for NLP
- ![](https://i.imgur.com/DlSXUje.png)
## Issues with Recurrent Models 
- **Linear Interaction Distance**
	- RNNs are unrolled "<font color="#d99694">left-to-right</font>"
		- This encodes **linear locality** : a useful heuristic
		- Nearby words often affect each other's meanings
	- Problem
		- RNN take $O(\text{sequence length})$ steps for distant word pairs to interact.
		- ![](https://i.imgur.com/b0jvB2v.png)
			- Info of *chef* has gone through $O(\text{sequence length})$ many layers!
		- Hard to learn **long-distance dependencies**(gradient problems)
		- Linear order of words is "baked in" ; however we know linear order may not be the best way to think about sentences
- ***<font color="#d99694">Lack of Parallelizability</font>***
	- Forward and backward passes have $O(\text{sequence length})$ unparallelizable operations
		- GPUs can perform a bunch of independent computations at once
		- But future RNN hidden states can't be computed in full before past RNN hidden states have been computed
			- This inhibits training on very large datasets
			- ![](https://i.imgur.com/4Al8rwI.png)
