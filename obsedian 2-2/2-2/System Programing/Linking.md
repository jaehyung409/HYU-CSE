#compile
##### Ref : [링커 - GeeksforGeeks](https://www.geeksforgeeks.org/linker/?ref=gcse_outind)
### Static Linking
![](https://i.imgur.com/9JeFDEt.png)
### Why Linkers
1. Modularity
	- Program as a collection of smaller source files, rather than one monolithic mass.
	- Libraries of common functions (more on this later)
2. Efficiency
	- Time : Seperate compilation
		- Change one source file, compile, and then re-link
		- No need to recompile other source files (Independence)
	- Space : Libraries
		- Common functions can be aggregated into a single file
		- Yet executable files and running memory images contain only code for the functions they actually use

### What Do Linkers Do?
- Step 1. [[Symbol Resolution]]
- Step 2. [[Relocation]]
### [[Executable and Linkable Format]]
### [[Package]]
