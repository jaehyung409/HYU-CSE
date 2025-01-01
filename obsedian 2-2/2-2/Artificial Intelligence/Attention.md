## Attention
- Attention (mechanism) provides a solution to the [[Neural Machine Translation#^6fda58|bottleneck problem]]
	- Core idea : on each step of the decoder, use direct connection to the encoder to focus on a particular part of the source sequence
- Sequence-to-Sequence with Attention
	- ![](https://i.imgur.com/S7qnyuB.png)
	- ![](https://i.imgur.com/b21M84G.png)
	- ![](https://i.imgur.com/3S4LahS.png)
	- ![](https://i.imgur.com/DZzuyGc.png)
	- Procedure
		1. We have encoder hidden states $h_1,\cdots,h_N\in\mathbb{R}^h$
		2. On timestep $t$, we have decoder hidden state $s_t\in\mathbb{R}^h$
		3. We get the attention scores $e^t$ for this step$$e^t=[s_t^Th_1,\cdots,s_t^Th_N]\in\mathbb{R}^N$$
		4. We take softmax to get the attention distribution $\alpha^t$ for this step (this is a probability distribution and sums to 1)$$\alpha^t=softmax(e^t)\in\mathbb{R}^N$$
		5. We use $\alpha^t$ to take a weighted sum of the encoder hidden states to get the attention output $a_t$$$a_t=\sum_{i=1}^N\alpha_i^th_i\in\mathbb{R}^h$$
		6. Finally we concatenate the attention output $\alpha_t$ with the decoder hidden state $s_t$ and proceed as in the non-attention seq2seq model$$[\alpha_t:s_t]\in\mathbb{R}^{2h}$$
- Attention is Great
	- Attention significantly improves NMT performance
		- It is very useful to allow decoder to focus on certain parts of the source
	- Attention provides a more "human-like" model of the MT process
		- You can look back at the source sentence while translating, rather than needing to remember it all
	- Attention solves the bottleneck problem
		- Attention allows decoder to look directly at source; bypass bottleneck
	- Attention helps with the vanishing gradient problem
		- Provides shortcut to faraway states
	- Attention provides some interpretability (black-box)
		- By inspecting attention distribution, we see what the decoder was focusing on
		- We get (soft) alignment for free
			- This is cool because we never explicitly trained an alignment system
			- The network just learned aligment by itself
	- You can use attention in **many architectures and many tesks**
- <font color="#e5b9b7">More general definition of attention</font>
	- Given a set of vector <font color="#e5b9b7">values</font>, and a vector <font color="#e5b9b7">query, attention</font> is a technique to compute <u>**a weighted sum of values,** dependent on the query</u>
		- We sometimes say that the query attends to the values
			- Ex, in the seq2seq + attention model, each decoder hidden state (query) attends to all the encoder hidden states (values)
	- Intuition
		- The weighted sum is a <font color="#e5b9b7">selective summary</font> of the information contained in the values, where the query determines which values to focus on
		- Attention is a way to obtain a <font color="#e5b9b7">fixed-size representation of an arbitrary set of representations</font> (the values), dependent on some other representation (the query)
	- Conclusion
		- Attention has become the powerful, flexible, general way pointer and memory manipulation in all deep learning models.
## Self-Attention
- Problem : [[Recurrent Models for NLP]]
	- How about Attention
		- Attention treats each word's representations as a <font color="#d99694">query</font> to access and incorporate information from <font color="#d99694">a set of values</font>
			- Now we'll think about attention **within a single sentence**
				- <font color="#d99694">Self-Attention</font>
			- For attention, number of unparallelizable operations does not increase with sequence length
			- Maxumum interaction distance: $O(1)$, since all words interact at every layer
				- ![](https://i.imgur.com/Zrxmu6K.png)
	- Attention as a Soft, Averaging Lookkup Table
		- ![](https://i.imgur.com/SxDWVoc.png)
		- Example
			- ![](https://i.imgur.com/J8t2NuH.png)
- Let $w_{1:n}$ be a sequence of words in vocabulary $V$
- For each $w_i$, let $x_i=Ew_i$, where $E\in\mathbb{R}^{d\times|V|}$ is an embedding matrix
	1. Transform each word embeding with weight matrices $Q, K, V$, each in $\mathbb{R}^{d\times d}$
		- $q_i=Qx_i$ (queries)
		- $k_i=Kx_i$ (keys)
		- $v_i=Vx_i$ (values)
	2. Compute pairwise similarities between keys and queries ; normalize with softmax $$e_{ij}=q_i^Tk_j\qquad\qquad\alpha_{ij}=\frac{exp(e_{ij})}{\sum_{j'}exp(e_{ij'})}$$
	3. Compute output for each word as weighted sum of values$$o_i=\sum_j\alpha_{ij}v_i$$
- #### Barriers & solutions for Self-Attention
	- ![](https://i.imgur.com/8yDHmV5.png)
## Self-Attention as a Building Block
- ![](https://i.imgur.com/mdNge1O.png)
- Fixing the First Self-Attention Problem : Sequence Order
	- Since self-attention doesn't build in <font color="#d99694">order information</font>, we need to encode the oreder of the sentences in our keys, queries, and values
	- Consider representing each sequence index as a vector$$p_i\in\mathbb{R}^d\ \text{for }i\in{1,2,\cdots,n}\ \text{are position values}$$
		- Easy to incorporate this information into our self-attention block
			- just add the $p_i$ to our inputs
		- Recall that $x_i$ is the embedding of the word at index $i$$$\tilde x_i=x_i+p_i$$
	- Sinusoidal position representations
		- Concatenate sinusoidal functions of varying periods
		- The method proposed in the original Transformer paper
		- ![](https://i.imgur.com/2Moj81o.png)
		- Pros
			- Periodicity indicates that maybe "absolute position" isn't as important
			- Maybe can extrapolate to longer sequences as periods restart
		- Cons
			- Not learnable ; also the extrpolation doesn't really work
	- Vectors Learned from Scratch
		- Learned absolute position representations
			- Let all $p_i$ be learnable parameters
				- learn a matrix $p\in\mathbb R^{d\times n}$, and let each $p_i$ be a column of that matrix
				- Most system use
			- Pros 
				- Flexibility : each position gets to be learned to fit the data
			- Cons
				- Definitely can't extrapolate to indices outside $1,\cdots,n$ (<font color="#d99694">max length</font>)
		- Sometime people try more flexible representation of position
			- Relative linear position attention
			- Dependency syntax-based position
- Adding Non-Linearities in Self-Attention
	- Note that there are no elementwise nonlinearities in self-attention
		- Stacking more self-attention layers just <font color="#d99694">re-averages</font> value vectors
	- Easy fix 
		- Add a feed-forward network to post-process each output vector
		- ![](https://i.imgur.com/UQFFbIk.png)
		- $m_i=MLP(output_i)=W_2\cdot ReLU(W_1output_i+b_1)+b_2$
- Masking the Future in Self-Attention
	- To use self-attention in decoders, we need to ensure we can't peek at the future
		- ![](https://i.imgur.com/umlTL9G.png)
- Necessities for a Self-Attention Building Block
	- ![|300](https://i.imgur.com/J0Lh0Ax.png)
	- Self-Attention
		- The basis of the method
	- Position representations
		- Specify the seqeunce order, since self-attention is an unordered function of its inputs
	- Nonlinearities
		- At the output of the self-attention block
		- Frequently implemented as a simple feed-forward network
	- Masking
		- In order to parallelize operations while not looking at the future
		- Keeps information about the future from "leaking" to th past
