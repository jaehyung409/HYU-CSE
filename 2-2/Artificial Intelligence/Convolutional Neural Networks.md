## Convolutional Neural Networks (CNN)
- Recap : Fully Connected Layer 
	- ![](https://i.imgur.com/kiEe2HZ.png)
- ### Convolution Layer
	- ![](https://i.imgur.com/OJbajUZ.png)
	- ![](https://i.imgur.com/k2l1IIN.png)
	- ![](https://i.imgur.com/9ZeM0jp.png)
	- ![](https://i.imgur.com/0FkjFuf.png)
	- A Closer Look at Spatial Dimensions
		- $$\frac{N-F}{stride}+1$$
			- Input volume : N, filter-size : F
		- $$\frac{N+2P-F}{stride}+1$$
			- Pad with $P$ pixel
			- Why Padding
				- check edge case, control stride, enhance stabiilty
		- Number of Parameters
			- ![](https://i.imgur.com/mjpHPIo.png)
				- $$F^2CK\ \text{weights} + K\ \text{biases}$$
	- ![](https://i.imgur.com/XUCFaOI.png)
		- An activation map is a 28x28 sheet of neuron outputs
			1. Each is connected to a small region in the input
			2. All of them share parameters
- ### Pooling Layer
	- Makes the representations <font color="#d99694">smaller and more manageable</font>
	- Operates over each activation map independently
	- Max Pooling
		- ![](https://i.imgur.com/RtbbjNx.png)
	- ![](https://i.imgur.com/mWua0bc.png)
- ### Fully-Connected Layer (FC Layer)
	- Contains neurons that connect to the entire input volume, as in ordinary feedforward neural networks
- ### Convolution Networks
	- ![](https://i.imgur.com/TMABpy7.png)
		- Trend towards smaller filters and deeper architectures
		- Trend towards getting rid of POOL/FC layers (just CONV)
## Representative CNN Architectures
- VGGNet
	- Small filters, deeper networks
- ResNet
	- Very deep networks using residual connections
		- too many layer can make vanish problem
			- Sol)  
				- ![|200](https://i.imgur.com/lNLH9mP.png)

## Simple History
- Gradient-based learning applied to document recongnition
	- LeCun, Bottou, Bengio, Haffner 1998
		- ![](https://i.imgur.com/08pOBSj.png)
- Imagenet classification with deep convolutional neural networks
	- calle "AlexNet"
- Used in
	- Classification, Retrieval, Detection, Segmentation, Image Captioning, Style Transfer, self-driving Cars ...