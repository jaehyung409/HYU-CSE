#datastructure #segment_tree #algorithms
## Build 
```cpp
int build(int Node, int Start, int End){
	if (Start == End) return SegmentTree[Node] = Arr[Start];
	
	int Mid = (Start + End) / 2;
	int Left_Res = build(Node * 2, Start, Mid);
	int Right_Res = build(Node * 2 + 1, Mid + 1, End);
	
	return SegmentTree[Node] = Left_Res + Right_Res;
}
```