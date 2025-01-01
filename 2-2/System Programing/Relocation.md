### Relocation
![](https://i.imgur.com/4MPewsu.png)
-  Merges separate code and data sections into single sections
	- Relocates symbols from their relative locations in the $\text{.o}$ files to their final absolute memory locations in the executable
	- Updates all references to these symbols to reflect their new positions
- Step 1. Relocating sections and symbold definition
- Step 2. Relocating symbol references within sections
### Relocation Entries
-  For code, data, relocatoin entries tells the linker how to modify the reference when it merges the object file into an executable.
	- ![](https://i.imgur.com/pzulmCv.png)
- Relocation $\text{.text}$ section 
	- ![](https://i.imgur.com/U73j2So.png) Using PC-relative addressing for sum(): <font color="#e5b9b7">0x4004e8 = 0x4004e3 + 0x5</font>
	- $\text{.text}$ section : use offset 
	- $\text{.data, .bss}$ section : use absolute address
### Relocatable vs. Executable
- ![](https://i.imgur.com/WiZIB0T.png)
