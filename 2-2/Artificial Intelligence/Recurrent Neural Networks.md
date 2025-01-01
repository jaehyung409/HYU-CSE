## Recurrent Neural Networks (RNN)
- Core idea
	- ![](https://i.imgur.com/7iZwnHc.png)
- ![](https://i.imgur.com/Xs5FLml.png)
	- Advantages of RNNs
		- Can process input of <font color="#d99694">any length</font>
		- Computation for step $t$ can (in theory) use information from many step back
		- <font color="#d99694">Model size does not increase</font> for longer input context
		- <font color="#d99694">Same weights applied on every timestep</font>, so theere is symmetry how inputs are processed
## Training an RNN Language Model
- Procedure
	- Get a big corpus of text which is a sequence of words $x^{(1)},\cdots,x^{(T)}$
	- Feed into RNN-LM; compute output distribution $\hat y^{(t)}$ <font color="#d99694">for every step t</font>
		- i.e., predict probability distribution of every word, given words so far
	- Loss function on step $t$ is cross-entropy between predicted probability distribution $\hat y^{(t)}$, and the true next word $y^{(t)}$ (one-hot for $x^{(t+1)}$) $$J^{(t)}(\theta)=CE(y^{(t)},\hat y^{(t)})=-\sum_{w\in V}y_w^{(t)}\log\hat y_w^{(t)}=-\log\hat y_{t+1}^{(t)}$$
	- Average this to get overall loss for entire training set$$j(\theta)=\frac{1}{T}\sum_{t=1}^TJ^{(t)}(\theta)=\frac{1}{T}\sum_{t=1}^T-\log\hat y_{t+1}^{(t)}$$
	- ![](https://i.imgur.com/pcQOotn.png)
	- However, Computing loss and gradients across <font color="#c4bd97">entire corpus</font> $x^{(1)},\cdots,x^{(T)}$ is <font color="#c4bd97">too expensive</font>
- In practice, consider $x^{(1)},\cdots,x^{(T)}$ as a sentence (or a document)
	- Stochastic Gradient Descent allows us to compute loss and gradients for small chunk of data, and update
	- Compute loss $J(\theta)$ for a sentence (actually, a batch of sentences), compute gradients and update weights. Repeat
## Variants of RNN
- Bidirectional RNN and Multi-Layer RNN : Motivation
	- ![](https://i.imgur.com/4SYYkC8.png)
	- [[Bidirectional RNN]]
	- [[Multi-Layer RNN]]
- [[Long Short-Term Memory RNN]]
## [[Recurrent Models for NLP]]
## Applications of RNN
1. Generating Text with an RNN Language Model
	- ![](https://i.imgur.com/nH6GjRi.png)
	- ![](https://i.imgur.com/k9lHo1P.png)
2. Can be Used for Tagging
	- ![](https://i.imgur.com/fPrxgd2.png)
3. Can be Used for Sentence Classification
	- ![](https://i.imgur.com/Q3Mpg79.png)