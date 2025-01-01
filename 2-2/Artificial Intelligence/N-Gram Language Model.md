## N-Gram Language Model
- N-Gram Language Models are a fundamental and classic (before deep learning) way of implementing LMs
- An <font color="#d99694">n-gram</font> is a chunk of $n$ consecutive words
	- <font color="#d99694">Uni</font>grams : "a", "b", "c", "d"
	- <font color="#d99694">Bi</font>grams : "a b", "b c", "c d"
	- <font color="#d99694">Tri</font>grams : "a b c", "b c d"
	- <font color="#d99694">Four-</font>grams : "a b c d"
	- Idea 
		- Collect statistics about how frequent different n-grams are and use these to predict next word
- Markov assumption
	- ![](https://i.imgur.com/H2tGlVN.png)
- How do we get these n-gram and (n-1)-gram probabilities
	- By counting them in some large corpus of text (statistical approximation)$$\frac{P(x^{(t+1)},x^{(t)},\cdots,x^{(t-n+2)}}{P(x^{(t)},\cdots,x^{(t-n+2)})}=\frac{count(x^{(t+1)},x^{(t)},\cdots,x^{(t-n+2)}}{count(x^{(t)},\cdots,x^{(t-n+2)})}$$
- Example
	- ![](https://i.imgur.com/yNbcqA2.png)
		- As N increases, accuracy improves, but if it becomes too high, the number of examples decreases, reducing efficiency
## Generating Text-wtih a N-Gram Language Model
- ![](https://i.imgur.com/xKF7SWw.png)
	- ![](https://i.imgur.com/WOONED1.png)
