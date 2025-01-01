#compile 
### Three Kinds of Object Files (Modules)
- Relocatable object file ($\text{.o}$ file)
    > Contains code and data in a form that can ve combine with other relocatable object files to form executable object file
    > - Each $\text{.o}$ file is produced from exactly one source ($\text{.o}$) file
- Executable object file ($\text{a.out}$ file)
	> Contains code and data in a form that can be copied directly into memory and then executed
- Shared object file ($\text{.so}$ file)
	> Special type of relocatables object file that can be loaded into memory and linked dynamically, at either load time or run-time
	> Called _Dynamic Link Libraries_ (DLLs) by Windows

### Shared Libraries
- Static Libraries