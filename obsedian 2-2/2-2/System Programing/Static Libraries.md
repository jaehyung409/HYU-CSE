### Static libraries
- <font color="#e5b9b7">Static libraries</font> (in $\text{.a}$ archieve files)
	- Concatenate related ***relocatable object files into a single file*** with an index (called an <font color="#fac08f">archive</font>)
	- Enhance linker so that it tries to resolve unresolved external references by looking for the symbols in one or more archives
	- If an archive member file resolves reference, link it into the executable
- Linking with Static libraries (how to operate)![](https://i.imgur.com/2Qp8mno.png)
- Commonly Used Libraries
	- $\text{libc.a}$ : the C standard library
	- $\text{libm.a}$ : the C math library
- build
```Linux
gcc -c addvec.c multivec.c
ar rs libvector.a addvec.o multvec.o   // build static libraries
gcc -L. lab04.c -lvector -o lab04      // compile with static lib
```
### Creating Static libraries
- Archivers allow incremental updates
- Recompile functions that changed and replace $\text{.o}$ file in archive![](https://i.imgur.com/fwhRIbS.png)
### Using Static Libraries
- Compile time linking
- Linker's algorithm for resolving external references
	- Scan $\text{.o}$ files and $\text{.a}$ files in the command line order
	- During the scan, keep a list of the current unresolvec references
	- As each new $\text{.o}$ or $\text{.a}$ file, *obj*, is encountered, try to resolve each unresolved reference in the list against the symbols defined in *obj*
	- If any entries in the unresolved list at end of scan, then error
		- ![](https://i.imgur.com/03twrDz.png)
- Problem
	- Command line order matters
	- Moral : Put libraries at the end of the command line
### disadvantages 
- Duplication in the stored executables (every function needs libc)
- Duplication in the running executables
- Minor bug fixes of system libraries require each application to explicitely relink