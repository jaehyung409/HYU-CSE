## Fixed-Window Neural Language Model
- ![](https://i.imgur.com/g5btcYJ.png)
	- Imporvements over n-gram LM
		- No sparsity problem
		- Don't need to store all observed n-grams
	- Remaining problems
		- Fixed winodw is too small
		- Enlarging window enlarges $W$
		- Window can never be large enough
		- $x^{(1)}$ and $x^{(2)}$ are multiplied by completely different weights in $W$
			- We need a neural architecture that can process any lengthy input