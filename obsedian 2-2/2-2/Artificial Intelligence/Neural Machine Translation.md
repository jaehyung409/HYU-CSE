## Machine Translation
- Is the task of translating a sentence x from one languaeg (the **source language**) to a sentence y in another language (the **target language**)
## Sequence-to-Sequence
- The general notion here is an <font color="#e5b9b7">encoder-decoder</font> model
	- One neural network takes input and produces a neural representation
	- Another network produces output based on that neural representation
	- If the input and output are sequences, we call it a seq2seq model
- Sequence-to-sequence is useful for more than just MT; many NLP tasks can be phrased as sequence-to-sequence
	- **Summarization** (long text $\rightarrow$ short text)
	- **Dialogue** (previous utterances $\rightarrow$ next utterance)
	- **Code generation** (natural language $\rightarrow$ Python code)
- It is an example of a conditional language model
	- **Language model** because the decoder is predicting the next word of the target sentence $x$
	- **Conditional** because its predictions are also conditional on the source sentence $x$
- The Bottleneck Problem of Seq2Seq ^6fda58
	- ![](https://i.imgur.com/ud3fxAg.png)
## Neural Machine Translation (NMT)
- Is a way to do Machine Translation with a **single end-to-end neural network**
	- The neural network architecture is called a <font color="#e5b9b7">*sequence-to-sequence*</font> model and it involvs two [[Recurrent Neural Networks]]
	- ![](https://i.imgur.com/5Ge5YHU.png)
- NMT directly calculates (encoding $\rightarrow$ decoding)
	- ![](https://i.imgur.com/HQY5XuQ.png)
## Training a Neural Machine Translation System
- Get a big paralled corpus (such as En $\leftrightarrow$ Kor)
	- ![](https://i.imgur.com/Yl8JVB8.png)
- But there is exciting work on unsupervised NMT, data augmentation, etc.