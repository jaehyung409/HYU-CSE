#algorithms 
ref : 
- [Potential Method in Amortized Analysis - GeeksforGeeks](https://www.geeksforgeeks.org/potential-method-in-amortized-analysis/?ref=header_outind)
- Introduction to algorithms, 3rd.
## Potential method
>We will perform n oprations
>- $D_0$ : an initial data structure
>- $D_i$ : the data structure that results after applying the *i*th opration to data structure $D_{i-1}$
>
>Potential difference $\Phi(D_i) -\Phi(D_{i-1})$
>- positive : The potential of the data structure increases
>- negative : The decrease in the potential pays for the actual cost of the opration
>
>Amortized cost $\hat{c}_i=c_i+\Phi(D_i)-\Phi(D_{i-1})$ ; $\Phi(D_i)\geq\Phi(D_0)\ \text{for all }i$
- Vs. accounting method
	- Similar to the accounting method
	- Differs from the accounting method in that
		- "potential energy" or just "potential" is used instead of credit
	- In the accounting method, each credit is associated with a specific object within the data structure
	- In the potential method, the potential is associated with the whole data structure
### 1. Example of stack operation
| operations  | The actual costs | $\Phi(D_i)-\Phi(D_{i-1})$ | The amortized costs |
| ----------- | ---------------- |:------------------------- | ------------------- |
| PUSH        | 1                | 1                         | 2                   |
| POP         | 1                | -1                        | 0                   |
| MULTIPOP(k) | min(k,s)         | -min(k,s)                 | 0                   |
### 2. Example of incrementing binary counter
- Potential function $\Phi(D_i) = b_i$
	- The number of 1s in the counter after the *i*th INCREMENT operation
- $t_i$ : The numver of bits reset in the *i*th INCREMENT opration
- The *i*th operation resets $t_i$ bits and sets at most 1 bit
![](https://i.imgur.com/JTwMlP8.png)
![](https://i.imgur.com/tB136c3.png)
![](https://i.imgur.com/VXkjI42.png)
