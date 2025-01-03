## Transformer
- A neural architecture designed <font color="#d99694">only with the attention mechanism</font> (No CNNs or RNNs)
	- The <font color="#d99694">self-attention mechanism</font> lies at its core
	- It enables parallel computations of representations $\Rightarrow$ Scalability$\uparrow$
	- Also originally proposed for machine translation (the **seq2seq** architecture)
	- ![|400](https://i.imgur.com/2DTzvis.png)
- ![|400](https://i.imgur.com/O5aYt3V.png)
## Transformer Decoder
- A Transformer decoder is how we'll build systems like language models
	- It's a lot like our minimal self-attention architecture, but with **a few more componenets**
	- The embeddings and position embeddings are identical
- Sequence-Stacked Form of Attention
	- Let $X=[x_1;\cdots;x_n]\in\mathbb{R}^{n\times d}$ be the concatenation if input vectors
		- $XK\in\mathbb{R}^{N\times d}$ (key), $XQ\in\mathbb{R}^{N\times d}$ (query), $XV\in\mathbb{R}^{N\times d}$ (value)
		- ![](https://i.imgur.com/EGTr8yw.png)
- Multi-Head Attention
	- ![](https://i.imgur.com/yc6zi5m.png)
	- We'll define <font color="#d99694">multiple attention "heads"</font> through multiple $Q,K,V$ matrices
		- Let $Q_l,K_l,V_l\in\mathbb{R}^{d\times\frac{d}{h}}$, where $h$ is the  number of attention heads, and $l$ ranges from $1$ to $h$
		- Each attention head performs attention independently$$output_i=softmax(XQ_lK_l^TX^T)*XV_l,\ \text{where }output_l\in\mathbb{R}^{d/h}$$
		- Then the outputs of all the heads are combined$$output=[output_1;\cdots;output_h]Y,\ \text{where }Y\in\mathbb{R}^{d\times d}$$
		- Each head gets to "look" at different things, and construct value vectors differently
	- Even though we computs $h$ many attention heads, it's not really more costly
		- We compute $XQ\in\mathbb{R}^{n\times d}$, and then reshape to $\mathbb{R}^{n\times h\times\frac{d}{h}}$ (Likewise for $XK, XV$)
		- Then we transpose to $\mathbb{R}^{h\times n\times\frac{d}{h}}$
		- Almost everything else is identical, and the **matrices are the same sizes**
		- ![](https://i.imgur.com/TXtLeDe.png)
- <font color="#d99694">Scaled Dot Product</font> attention aids in training
	- When dimensionality $d$ becomes large, dot products between vectors tend to become large
	- Because of this, inputs to the softmax function can be large, making the gradients small
	- Solution
		- Instead of the self-attention function we've seen$$output_l=softmax(XQ_lK_l^TX^T)*XV_l$$
		- We divide the attention scores by $\sqrt{d/h}$, to stop the scores from becoming large just as a function of $d/h$ (the dimensionality divided by the number of heads)$$output_l=softmax(\frac{XQ_lK_l^TX^T}{\sqrt{d/h}})*XV_l$$
- Two optimizations tricks
	- ![](https://i.imgur.com/Frhxv1u.png)
	- Residual Connections (help models train batter)
		- Instead of $X^{(1)}=Layer(X^{(i-1)}$ (where $i$ represents the layer)
			- ![](https://i.imgur.com/hcQ3xQd.png)
		- We let $X^{(1)}=X^{(i-1)}+Layer(X^{(i-1)})$ (so we only have to learn "the residual" from the previous layer)
			- ![](https://i.imgur.com/Bfar8xh.png)
		- Gradient is **great** through the residual connection: It's 1
			- ![|300](https://i.imgur.com/BFDWUu1.png)
	- Layer Normalization (help models train faster)
		- **idea** : cut down on uninformative variation in hidden vector values by normalizing to unit mean and standard deviation within each layer
			- LayerNorm's success may be due to its normalizing gradients
		- Details
			- Let $x\in\mathbb{R}^d$ be an individual (word) vector in the model
			- Let $\mu=\frac{1}{d}\sum_{j=1}^dx_j$ ; this is the mean $\mu\in\mathbb{R}$
			- Let $\sigma=\sqrt{\frac{1}{d}\sum_{j=1}^d(x_j-\mu)^2}$ this is the standard deviation; $\sigma\in\mathbb{R}$
			- Let $\gamma\in\mathbb{R}^d$ and $\beta\in\mathbb{R}^d$ be learned "gain" and "bias" parameters (Can omit)
			- Then layer normalization compute
				- ![](https://i.imgur.com/0YJDbqT.png)
- ![](https://i.imgur.com/WI2H6uJ.png)
## Transformer Encoder
- The Transformer Decoder constrains to **undirectional context**, as for **language models**
- The **Transformer Encoder**. The only difference is that we <font color="#d99694">remove the masking</font> in the self-attention
	- ![|400](https://i.imgur.com/5XMhKFg.png)
## Transformer Encoder-Decoder
- For this kind of seq2seq format, we often use a **Transformer Encoder-Decoder**
	- We use a normal Transformer Encoder. 
	- Our Transformer Decoder is modified to perform crossattention to the output of the Encoder. 
	- ![|400](https://i.imgur.com/DNBgwtO.png)
- Cross-Attention
	- We saw that self-attention is when keys, queries, and values come from the same source
	- In the decoder, we have attention that looks more like what we saw perviously
		- Let $h_1,\cdots,h_n$ be **output** vectors **from** the Transformer **encoder** $h_i\in\mathbb{R}^d$
		- Let $z_1,\cdots,z_n$ be **input** vectors **from** the Transformer **decoder** $z_i\in\mathbb{R}^d$
		- Then **keys** and **values** are drawn from the **encoder** (like a memory) $$k_i=Kh_i,\ v_i=Vh_i$$
		- And the **queries** are drawn from the **decoder**, $q_i=Qz_i$

	- ![](https://i.imgur.com/1gVQXEg.png)
