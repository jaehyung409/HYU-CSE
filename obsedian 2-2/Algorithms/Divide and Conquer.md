#algorithms #divied_and_conquer 

## Ref : [[Recurrence]]

$$
T(n) = \begin{cases}\Theta(1) \qquad \quad \qquad \qquad if \ n = 1, \\ 2T(n/2) +\Theta(n) \qquad if \: n > 1 \end{cases} \quad =\Theta log(n)
$$
Solve with 
### The substitution method
1. Suppose : $T(n) \leq cn\lg n$ 
2. Assume that $T\lfloor n/2\rfloor \leq c\lfloor n/2\rfloor \lg(\lfloor n/2\rfloor)$
3. Inductive step
	$$\begin{align} T(n) & = 2T\lfloor n/2\rfloor + n \leq 2(c\lfloor n/2\rfloor \lg(\lfloor n/2\rfloor)) + n \\
& \leq cn\lg(n/2)+n \\
&=cn\lg n - cn\lg 2 + n\\
&=cn\lg n - cn + n\\
&\leq cn\lg n\\
&\ (as\ long\ as\ c \geq 1)
\end{align}
$$
4. Boundary conditions
	- $T(n) \leq cn\lg n \ for\ n = 1(?)$
		- It is impossible  because $T(1) = 1\ but\ c 1 \lg 1 = 0$
5. Any choice of $c \geq 2$ satisfies the inequality for $n \geq \ n_0\ for\ n_0 = 2$ 

### Recursion-tree method
1. ![](https://media.geeksforgeeks.org/wp-content/uploads/20210608083944/img-300x172.PNG)
2. ![](https://media.geeksforgeeks.org/wp-content/uploads/20210608091942/img1-300x141.PNG)
3. Tree level(height) : $\log_2 n + 1$, Last level Cost : $n*\Theta(1) = \Theta(n)$
4. T(n) = $\sum_1^{\log_2(n)}c + \Theta(n)$ = $\Theta(n\lg n)$