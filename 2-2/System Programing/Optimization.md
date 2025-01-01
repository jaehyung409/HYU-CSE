
## Generally Useful Optimizations
> #### <font color="#fac08f">"Equivalent"</font>, Can compiler optimizations
- #### 1. Code Motion (-o1)
> Reduce frequency with which computation performance
![](https://i.imgur.com/vdn1w2U.png)
- #### 2. Reduction in Strength
> Replace costly operation with simpler one
![](https://i.imgur.com/biAMmHx.png)
- #### 3. Share Common Subexpressions (-o1)
> Reuse portions of expression
![](https://i.imgur.com/8ZLb6mP.png)
- #### 4. Removing unnecessary procedure calls
## Optimization Blockers
- #### 1. Procedure Calls
> Compiler treats procedure call as a black box 
![](https://i.imgur.com/HDsYiHT.png)
![](https://i.imgur.com/mBawPlO.png)
- #### 2. Memory Aliasing
> Aliasing : Two different memory references specify single location
> Get in habit of introducing local variables (telling compiler not to check for aliasing)