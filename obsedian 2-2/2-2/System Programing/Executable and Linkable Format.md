## ELF
- Executable (output of linker), Linkable (input of linker) In same ELF (same format)
- Standard binary format for object files in Linux
	- Different systems use different format
	- But concepts are very similar
- <font color="#fac08f">One unified format</font> for three kinds of Object Files![[Object Files#Three Kinds of Object Files (Modules)]]
- Generic name $\rightarrow$ ELF binaries

## ELF Object File Format
| ELF Object File Format                          | explanation                                                                                                                                       |
| ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| ELF header                                      | Word size, byte ordering, file type(.o, exec, .so), machine type, etc.                                                                            |
| Segment header table (required for executables) | Page size, virtual addresses memory segmants(sections), segment sizes                                                                             |
| $\text{.text}$ section                          | Code                                                                                                                                              |
| $\text{.rodata}$ section                        | Read only data: jump tables,...                                                                                                                   |
| $\text{.data}$ section                          | Initialized global variables                                                                                                                      |
| $\text{.bss}$ section                           | 1. Uninitialized golbal variables  2. "Block Started by Symbol" 3. Has section header but occupies no space                                       |
| $\text{.symtab}$ section                        | 1. Symbol table 2. Procedure and static variables names 3. Section names and locations                                                            |
| $\text{.rel.txt}$ section                       | 1. Relocation info for $\text{.text}$ section 2. Addresses of instructions that will need to be modified in the executable 3. Instructions for modifying |
| $\text{.rel.data}$ section                      | 1. Relocation info for $\text{.data}$ section 2. Addresses of pointer data that will need to be modified in the merged executable                        |
| $\text{.debug}$ section                         | info for symbolic debugging (**gcc -g**)                                                                                                          |
| Section header table                            | Offsets and sizes fo each section                                                                                                                                                  |

## Loading Executable Object Files
![](https://i.imgur.com/lfcdFdn.png)
