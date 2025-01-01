#greedy #algorithms 

reference : 
- [허프만 코딩 | Greedy Algo-3 - GeeksforGeeks](https://www.geeksforgeeks.org/huffman-coding-greedy-algo-3/?ref=gcse_outind)
- Introductions to algorithms, 3rd

### Huffman Codes 
>  - A widely used technique for compressing data
>  - Huffman invented a greedy algorithm that constructs an optimal prefix code called an Huffman code
- Prefix codes
	- No codeword is a prefix of some other codeword (remove ambiguous)
	- ![](https://media.geeksforgeeks.org/wp-content/uploads/20220906180456/6.png)
	- ***full binary tree*** for alphabet set C has n(C) leaves and n(C)-1 internal nodes

| character   | f   | c   | d   | a    | b    | e   |
| ----------- | --- | --- | --- | ---- | ---- | --- |
| code-word   | 0   | 100 | 101 | 1100 | 1101 | 111 |
| frequencies | 45  | 12  | 13  | 5    | 9    | 16  |
- The cost fo tree T
	- $f(c)$ : frequency of a character $c$
	- $d_T(c)$ : length of the codeword for $c$
	- $$B(T) = \sum_{c\in C}{f(c)d_T(c)}$$
	- An optimal code is represented by a full binary tree

### Greedy Algorithms
- using [[Heap|Min Heap]]
1. Create a leaf node for each unique character and build a Min Heap of all leaf nodes 
2. Extract two nodes with the minimum frequency from the Min Heap
3. Create a new internal node with a frequency equal to the sum of the two nodes frequencies. Add this node to the Min Heap
4. Repeat step2~3 until the heap contains only one node(root node)

### Performance
- Running time : $O(n\lg n)$
	- Build min heap : $O(n)$
	- Merge : $n-1$ times
		- Each merge requires two minimum selection(+ one insertion) : $O(\lg n)$

### Correctness
- ##### _Lemma 16.2_
	- Let $C$ be an alphabet in which each character $c\in C$ has frequency $f[c]$
	- Let $x$ and $y$ be two characters in $C$ having the lowest frequencies
	- Then there exists an optimal prefix code for $C$ in which <font color="#92cddc">_the codewords for x and y have the same length and differ only in the last bit._</font>

- ##### _Proof_
	- **Idea** : take an arbitary optimal prefix coed tree $T$ and modify it and to make a tree representing another optimal prefix code such that the characters $x\ \text{and }y$ apper as sibling leaves of maximum depth in the new tree.
	- ![](https://i.imgur.com/VnMYGt8.png)
	- compute their cost(with $B(T) = \sum_{c\in C}{f(c)d_T(c)}$) and compare them.

- ##### _Lemma 16.3_
	- Let $x\ \text{and }y$ be two characters in a given alphabet $C$ with minimum frequency
	- Let $C^{'}$ be the alphabet $C$ with caracters $x, y$ removed and character $z$ added, so that $C^{'} = C - \{x,y\}\cup \{z\}$; define $f\ \text{for }C^{'}$ as for $C$, except that $f[z] = f[x] + f[y]$
	- Let $T^{'}$ be any tree representing an optimal prefix code for the alphabet $C{'}$
	- <font color="#92cddc">Then the optimal prefix code tree $T$ for $C$ can be obtained from $T^{'}$ by replacing the leaf node for $z$ with an internal node habing $x$ and $y$ as children.</font>

- ##### _Proof_
	- Show $B(T) = B(T^{'} + f[x] + f[y]$
		- For each $c\in C- \{x,y\}$, we have $d_T(c)$, and hence $f[c]d_T(c) = f[c]d_T(c)$
		- Since $d_T(x) = d_T(y) = d^{'}(z) + 1$, we have $$\begin{align}f[x]d_T(x) + f[y]d_T(y) &=(f[x] + f[y])(d_{T^{'}}(z) + 1) \\ &= f[z]d_{T^{'}}(z) + (f[x] + f[y])\end{align}$$
		- From which we conclude that $B(T) = B(T^{'})+f[x]+f[y]$ or, equivalently $B(T^{'}) = B(T)-f[x]-f[y]$
	- ![](https://i.imgur.com/0dnXhsE.png)
	- Contradiction
		- Let $T$ is not an optimal prefix code tree.
		- Than, there exits a tree $T^{''}$ such that $B(T^{''}) < B(T)$
		- By Lemma 16.2, $T^{''}$ has sibling leaves $x\ \text{and }y$
		- Let $T^{'''}$ be the tree obtained by replacing the common parent of $x$ and $y$ with $z$ in $T^{'''}$
		- This constradicts the assumption
