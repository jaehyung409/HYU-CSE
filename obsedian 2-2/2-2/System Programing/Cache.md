### ref : 
- [[Memory Hierarchies]]
## General Cache Concepts
![](https://i.imgur.com/YeXK9GY.png)
- Fundamental idea of a memory hierarchy
	- Placing a subset of data in slower storage to faster storage
	- For each k, storage at level k serves as a cache for storage at level k+1
- What makes memory hierarchies work effecively
	- More every accessed data to faster storage
	- Evict less frequently accessed data from faster storage
	- Then frequently accessed data will be left in faster storage
- Big idea
	- All data can be stored in a large pool of storage
	- A subset of data can be accessed at speed of the fastest storage
- Data is copied to faster memory at every access $\rightarrow$ temporal
- Tranfering more data than requested $\rightarrow$ spatial
## Cache Hits
- ![](https://i.imgur.com/I4ByGbD.png)
## Cache Misses
- ![](https://i.imgur.com/ArnHMz5.png)
- ### Types of Caches Misses (a.k.a 3c)
	- <font color="#fac08f"> Cold miss (or compulsory miss)</font>
		- Cold misses occur because the cache is empty
	- <font color="#fac08f">Conflict miss</font>
		- Most caches limit blocks at leverl k+1 to a small subset of the block positions at level k
			- E.g., Block i at level k+1 must be placed in block (i mod 4) at level k
		- Conflict misses occur when the level k cache is large enough, but multiple data objects all map to the same level k block
			- E.g., Referencing blocks 0, 8, 0, 8, 0, 8, ... would miss every time
	- <font color="#fac08f">Capacity miss</font>
		- The set of active cache blocks (working set) is larger than the cache
## System Design 
- Related to Cache Misses
	- Cache organization of fixed size cache $$\text{Total size = Block size }\times\text{\# of blocks}$$
		- Increasing block size
			- Exploits better spartial locality
			- Makes cache faster by comparing fewer blocks for replacement
		- But decreasing \# of blocks
			- Increases **miss rate** due to eviction of more words
			- Increases **miss penalty** due to increased IO amount
- Related to Cache Writes
	- Using cache memory duplicates data
		- Data in caches and the same copy of the data in memory
	- What if change the data in cache?
		- **Write-through** : Updates data in both cache and memory
		- **Write-back** : Updates data only in cache, and later data in memory if **dirty bit** is on