#disjoint_set #linked_list #datastructure 
## Disjoint Sets (Linked List)
![](https://i.imgur.com/3ad56PH.png)
- The object for each set has two attributes *head* and *tail*
	- Attribute *head* points to the first object
	- Attribute *tail* points to the last object
- All objects have pointer to the set object
- The first object in the linked list is the representative

## Operations
- MAKE-SET(x) ($\Theta(1)$)
	- Create a new linked list whose only object is *x*
- FIND-SET(& x) ($\Theta(1)$)
	- Follow the pointer from *x* back to its set object and then return the member in the object that head points to
- UNION(&x, &y) ($\Theta(m_y)$ : $m_y$ is the number of objects of $y$) 
	- Attaching a linked list to the other  
	- ![](https://i.imgur.com/I8E769G.png)
	- Changing tail pointer  & linking two linked lists : $\Theta(1)$
	- Changing pointers to the set object : $\Theta(m_y)$

## Running time for BUILD
- Parameters 
	- Total Operaions : $m$
	- MAKE-SET ops : $n$
	- UNION ops : $u$
		- $u\leq n-1$ : Each UNION op reduces the number of sets by 1 
	- FIND-SET ops : $f$
	- $m = n + u + f$
- Simple implementation of union
	- $O(n+f+n^2)$ time -> $O(m+n^2)$
		- Because $u\leq n-1$
- A weighted-union heutistic (small element -> big element)
	- $O(n+f+u+n\lg n)$ time -> $O(m+n\lg n)$