## Language Modeling
- Language Modeling is the task of predicting what word comes next
	- Given a sequence of words $x^{(1)},x^{(2)},\cdots,x^{(4)}$ (context), compute the probability distribution of the next words $x^{(t+1)}$$$P(x^{(t+1)}|x^{(t)},\cdots,x^{(1)})$$ where $x^{(t+1)}$ can be any word in the <font color="#d99694">vocabulary</font> $V = {w_1,\cdots,w_{|v}}$
		- ![](https://i.imgur.com/R2lCF1x.png)
	- You can also think of a language model as a system that assigns <font color="#d99694">a probability to a piece of text</font>$$\begin{align}P(x^{(1)},\cdots,x^{(t)})&=P(x^{(1)})\times P(x^{(2)}|x^{(1)})\times\cdots\times P(x^{(T)}|x^{(T-1)},\cdots,x^{(1)})\\&=\Pi_{t=1}^TP(x^{(t)}|x^{(t-1)},\cdots,x^{(1)})\end{align}$$
-  What can we do with LMs 
	- Score sentences
	- Generate sentences
```pseudo
GENERATE_SENTENCES
	while didn't choose end-of-sentences symbol:
		Calculate probabaility
		Sample a new word from the probability distribution
```
## [[N-Gram Language Model]]
## [[Fixed-Window Neural Language Model]]
## [[Recurrent Neural Networks]]
