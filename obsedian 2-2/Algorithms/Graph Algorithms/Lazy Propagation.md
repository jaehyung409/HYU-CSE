#algorithms #segment_tree #range_sum 
## Lazy Propagation
> A speedup technique for range updates in [[Segment Tree]]
> Delay sum updates (avoid recursive calls in update) and do such updates only when necessary when there are several updates and updates are being performed on a range

## Array called Lazy\[]
- Size : Segment Tree.size()
- Element :
	- initial : 0
	- Update when Segment Tree.parent() update
		- Element = Element + $\delta x$
- Update Lazy (When Segment Tree->operation : visit lazy\[node] != 0)
	- Update Segment Tree.node()
	- Lazy children += Lazy\[node]
	- Lazy\[node] = 0
## Complexity $O(n)$