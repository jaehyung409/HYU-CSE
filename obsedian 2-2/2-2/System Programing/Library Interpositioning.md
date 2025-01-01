## Library interpositioning
- Powerful linking technique that allows programmers to intercept calls to arbitrary functions
- Interpositioning can occur at
	- Compile time : When the source code is compiled
	- Link time : When the relocatable object files are statically linked to form an executable object file
	- Load/Run time : When an executable object file is loaded into memory, dynamically linked, and then executed
## Applications
- Security
	- Confinement (sandboxing)
	- Behind the scenes encryption
- Debugging
- Monitoring and Profiling
	- Count number of calls to functions
	- Characterize call sites and arguments to functions
	- Malloc tracing
		- Detecting memory leaks
		- Generating address traces
## Compile time
- ![](https://i.imgur.com/mIAVRZ3.png)
	- Apparent calls to malloc/free get macro-expanded into calls to mymalloc/myfree
## Link time
- ![](https://i.imgur.com/zc92VeQ.png)
	- The` "-Wl"` flag passes argument to linker, replacing each comma with a space
	- The `"--wrap,malloc "` arg instructs linker to resolve references in a special way
		- Refs to malloc should be resolved as `__wrap_malloc`
		- Refs to `__real_malloc` should be resolved as `malloc`
## Load/Run time
- ![](https://i.imgur.com/XLYRsSe.png)
	- The `LD_PRELOAD` environment variable tells the dynamic linker to resolve unresolved refs (e.g., to `malloc`) by looking in `mymalloc.so` first
	- Implement custom version of malloc/free that use dynamic linking to load library malloc/free under different name