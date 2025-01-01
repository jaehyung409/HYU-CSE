#binary_search #lis 

### Ref : 
- [Longest Increasing Subsequence (LIS) - GeeksforGeeks](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/?ref=gcse_outind)
- [Longest Increasing Subsequence Size (N log N) - GeeksforGeeks](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/)
### Dynamic Programing $O(n^2)$
- Memoization
### Binary Search $O(n\lg n)$
1. vector\[0] = array\[0]
2. If array\[i] is bigger than last element of vector, add it end of the vector.
3. else, binary search to bucket (lower bound) and replace it.
![](https://i.imgur.com/tPAmqre.png)