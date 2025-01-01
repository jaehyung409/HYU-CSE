### Shared Libraries
- Object files that contain code and data that are loaded and linked into an application *dynamically*, at either *load-time* or *runtime*
- Also called : dynamic link libraries, $\text{.dll, .so}$ files
- build
```Linux
gcc -c addvec.c multvec.c
gcc addvec.o multvec.o -shared -o libvector.so // build shared lib
gcc -L. lab04.c -lvector -o lab05 // compile with shared lib
								  // higher priority than static lib
```
### Dynamic Linking
- Dynamic linking can occur when executable is first loaded and run (load-time linking)
	- Common case for Linux, handled automatically by the dynamic linker(**ld-linux.so**)
	- Standard C library (**libc.so**) usually dynamically linked
- Dynamic linking can also occur after program has begyn (run-time linking)
	- In Linux, this is done by calls to the **dlopen ()** interfcae
		- Distributing software
		- High-performance web servers
		- Runtime library interpositioning
- Shared library routines can be shared by multiple processes

### Dynamic Linking at Load-time
![](https://i.imgur.com/zfCPypN.png)
### Dynamic Linking at Run-time
 ![](https://i.imgur.com/b3ilW55.png)
![](https://i.imgur.com/o1XKNzy.png)
### Shared Libraries executable
- ![](https://i.imgur.com/eMgRAt2.png)
	- @plt : Procedure Linking Table
		- The address of jump target is in $\text{.data}$ section