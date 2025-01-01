#artificial_intelligence #linear_algebra #math 
### Baics; Linear Algebra (1)
> Linear algebra provides a way of compactly representing and operating on sets of linear equations

- Basic Concepts and Notation
	- Tensors : array of numbers, that may have
		- Scalars (zero dim)
		- Vectors (one dim)
		- Matrics (two dim)
	- Matrix Multiplication
		- $C_{ij} = \sum_{k=1}^{n}{A_{ik}B_{kj}}$
		- Vector-Vector Products
			- $x^Ty$ : <font color="#de7802">inner product</font> or <font color="#de7802">dot product</font> (scalar)
			- $xy^T$ : <font color="#de7802">outer product</font> of the vectors. (matrix)
		- Matrix-Vector Proucts $y = Ax \in \mathbb{R}^n$
			- **y** is a linear combination of the ***columns*** of $A$, where the coefficients of the linear combination are given by the entries of **x**. (**y**$^T$ -> **rows** of $A$)
		- 4 different ways of viewing ***Matrix-Matrix Products(multiplication)***
			0. The direct advantage of these various viewpoints is that they allow <font color="#92cddc">you to operate on the level/unit of vectors instead of scalars</font>.
			1. A set of vector-vector products
			- The $(i,j)$th entry of $C$ is equal to the inner product of the $i$th row of A and the $j$th column of B.
			  $$C=AB=\begin{equation} \begin{bmatrix} - & a_{1}^T & - \\ - & a_{2}^T & - \\ \vdots & \vdots & \vdots \\ - &a_m^T &- \end{bmatrix} \begin{bmatrix} | &| &\cdots &|\\b^1&b^2&\cdots&b^p\\|&|&\cdots&| \end{bmatrix} = \begin{bmatrix}a_1^Tb^1 &a_1^Tb^2&\cdots &a_1^Tb^p \\ a_2^Tb^1& a_2^Tb^2&\cdots&a_1^Tb^p\\ \vdots&\vdots&\ddots&\vdots\\a_m^Tb^1&a_m^Tb^2&\cdots&a_m^Tb^p \end{bmatrix}\end{equation}$$
			2. A sum of outer products
			- Represent A by columns, and B by rows.
			- AB is equal to the sum, over all $i$, of the outer product of the $i$th column of $A$ and the $i$th row of $B$
			  $$ C=AB=\begin{equation} \begin{bmatrix} | & | & & | \\ a^1 & a^2 & \cdots & a^n \\ | & | & & | \end{bmatrix} \begin{bmatrix} - & b_1^T & - \\ - & b_2^T & - \\ & \vdots & \\ - & b_n^T & - \end{bmatrix} \end{equation} = \sum_{i=1}^n{a^ib_i^T}$$
			3. A set of matrix-vector products
				- If we represent B by columns, we can view the columns of $C$ as matrix-vector products between $A$ and the columns of $B$
				- $c_i=Ab_i$
				  $$C=AB=A\begin{bmatrix} | & | & & | \\ b^1 & b^2 & \cdots & b^p \\ | & | & & |\end{bmatrix} = \begin{bmatrix} | & | & & | \\ Ab^1 & Ab^2 & \cdots & Ab^p \\ | & | & & |\end{bmatrix}$$
			4. Another set of matrix-vector products
				- We represent $A$ by rows, and view the rows of $C$ as the matrix-vector product between the rows of $A$ and $C$
				- $c_i^T=a_i^TB$
				  $$C=AB=\begin{bmatrix} - & a_1^T & - \\ - & a_2^T & - \\  & \vdots & \\ - & a_m^T & - \end{bmatrix}B = \begin{bmatrix} - & a_1^TB & - \\ - & a_2^TB & - \\  & \vdots & \\ - & a_m^TB & - \end{bmatrix}$$

### Operations and Properties
- Identity Matrix ; $$I_{ij} = \begin{cases}1 &i = j \\ 0& i \neq j \end{cases}$$
- Diagonal Matrix ; $$\begin{align} D &= diag(d_1,d_2 , ... ,d_n) \\ D_{ij} &= \begin{cases}d_i &i = j \\ 0& i \neq j \end{cases} \end{align} $$
- Transpose ; "flipping" $$(A^T)_{ij} = A_{ji}$$
	- Symmetric ; $$A = A^T$$
		- For any matrix $A\in \mathbb{R}^{n\times n}$,->sum of symmetirc + anti-symmetric
		- $$A = \frac{1}{2}(A + A^T) + \frac{1}{2}(A-A^T)$$
- Trace ; sum of D elements$$tr(A) = \sum_{i=1}^n{A_{ij}}$$
	- tr(ABC) = tr(BCA) = tr(CAB)
- Norm ; "length" of the vector $$\begin{align}||x||_2&=\sqrt{\sum_{i=1}^n{x_i^2}} \\||x||_p &= (\sum_i{|x_i|^p})^{\frac{1}{p}} \end{align}$$
	- In matrix, Frobenus norm$$||A||_F = \sqrt{\sum_{i=1}^m\sum_{j=1}^n{A_{ij}^2}} = \sqrt{tr(A^TA)}$$
- Linear Independence
	- c.f. linearly dependent $$x_n=\sum_{i=1}^{n-1}{a_ix_i}$$
- Rank (colum rank = row rank = rank, dimension)
- Inverse$$A^{-1}A = I = AA^{-1}$$
	- To have an inverse, A must be full rank (linearly Independent)
- Orthogonal$$x^Ty = 0$$
- Span $$span(\{x_1,...,x_n\}) = \Bigg\{v:v=\sum_{i=1}^n{a_ix_i},\ a_i\in\mathbb{R}\Bigg\}$$
- Projection, argmin means Orthogonal$$\text{Proj}(y;\{x_1,x_2,...,x_n\}) = \text{argmin}_{v\in\text{span}(\{x_1,...,x_n\})}||y-b||_2$$
	- Range (columnspace)
		- When $A\in\mathbb{R}^{m\times n}$ is full rank and $n < m$, the projection of a vector $y \in \mathbb{R}^m$ onto the range of $A$ is given by, $$\begin{align}\text{Proj}(y;A) &= \text{argmin}_{v\in\mathcal{R}(A)}{||v-y||_2} = A(A^TA)^{-1}A^Ty\\\text{Proj}(y;a)&=\frac{aa^T}{a^Ta}y\end{align}$$
	- Nullspace$$\mathcal{N}(A) = \{x\in\mathbb{R}^n : Ax = 0\}$$
	- $$\mathcal{R}(A^T) = \mathcal{N}(A)^{\bot}$$
- Determinant ; A function det : $\mathbb{R}^{n\times n} \rightarrow \mathbb{R}$ $$\begin{align}|A| &= \text{"volume" of the set }S\\ &= 0\ \{A\ \text{is singular, non-invertible}\} \\ &= \sum_{i=1}^n{(-1)^{i+j}a_{ij}|A_{\setminus i,\setminus j}|}\ (\text{for any }j\in 1,...,n)\\ &= \sum_{i=1}^n{(-1)^{i+j}a_{ij}|A_{\setminus i,\setminus j}|}\ (\text{for any }i\in 1,...,n) \end{align}$$
- Quadratic Forms ; Get the scalar value $$x^TAx = \sum_{i=1}^n{x_i(Ax)_i} = \sum_{i=1}^n{x_i\bigg(\sum_{j=1}^n{A_{ij}x_j\bigg)}=\sum_{i=1}^n{\sum_{j=1}^n{A_{ij}x_ix_j}}}$$
	- Note that,
		- $x^TAx=(x^TAx)^T=x^TA^Tx=x^T(\frac{1}{2}A+\frac{1}{2}A^T)x$
		- From this, we can conclude that only the symmetric part of A contributes to the quadratic form
		- For this reason, we often implicitly assume that the matrices appearing in a quadratic form are symmetric.
- Positive Definite
	- A symmetric matrix $A\in\mathbb{S}^n$ is <font color="#92cddc">positive definite</font> (PD)
		- if for all non-zero vectors $x\in\mathbb{R}^n,x^TAx>0$
		- This is usually denoted $A \succ 0$
		- The set of all positive definite matrices is denoted $\mathbb{S}_{++}^n$
	- Positive semidefinite (PSD)
		- $x^TAx\geq0, x\succcurlyeq,\mathbb{S}_+^n$
	- Negative definite (ND)
		- $x^TAx < 0, x\prec0$
	- Negative semidefinite (NS)
		- $x^TAx \leq 0, x\preccurlyeq0$
	- Indefinite
		- If it is neither positive semidefinite nor negative semidefinite
		- There exists $x_1,x_2\in\mathbb{R}^n$ such that $x_1^TAx_1>0\ \text{and }x_2^TAx_2<0$
	- PD and ND -> full rank (invertible)
	- Gram matrix$$A\in\mathbb{R}^{m\times n}, G = A^TA\ \text{is always positive semidefinite, (if }m\geq n\ \text{positive definite)}$$
	- Eigenvalues($\lambda$) and Eigenvectors($x$) $$(\lambda I - A)x = 0, x \neq 0$$
		- If $|(\lambda I-A)| = 0$, we can get Eigenvalues.
		- tr(A) = $\sum_{i=1}^n{\lambda}_i$
		- |A| =$\Pi_{i=1}^n{\lambda}_i$
		- The rank of A is equal to the number of non-zero eigenvalues of A
		- The eigenvalues of a diagonal matrix $D = diag(d_1,...,d_n)$ are just the diagonal entries $d_1, ..., d_n$
		- In Symmetric Matrices
			- All eigenvalues are real numbers
			- All eigenvectors are unit vectors and orthogonal to each other$$U=\begin{bmatrix}| & | & & | \\ u_1 &u_2 & \cdots & u_n \\ | &|& & |\end{bmatrix}$$
			- Let $\Lambda = diag(\lambda_1,...,\lambda_n), \Lambda U = U\Lambda$
				- $A=U\Lambda U^T$ <font color="#92cddc">(diagonalization or eigendecomposition)</font>
	- SVD (Singular Value Decomposition) ; general form of eigendecomposition. $$A = U\Sigma V^T = u_1\sigma_1v_1^T + ... u_r\sigma_rv_r^T$$
		![](https://i.imgur.com/5IUU1eP.png)
		- $U$ : orthogonal
		- $\Sigma$ : diagonal
		- $V$ : orthogonal
