#algorithms 
ref :
- [Accounting Method | Amortized Analysis - GeeksforGeeks](https://www.geeksforgeeks.org/accounting-method-amortized-analysis/?ref=header_outind)
- Introduction to algortihms, 3rd.
## Accounting method
> We want to show that in the worst case that average cost per operations is small by analyzing with amortized costs.
> - $c_i$ : actual cost of the *i*th operation
> - $\hat{c}_i$ : amortized cost of the *i*th operation
> - $\sum_{i=0}^n\hat{c}_i\geq\sum_{i=0}^nc_i$ : all sequence of *n* operations required
> - The total credit : $\sum_{i=0}^n\hat{c}_i-\sum_{i=0}^nc_i$

### 1. Example of stack operation
| operations  | The actual costs | The amortized costs         |
| ----------- |:---------------- | --------------------------- |
| PUSH        | 1                | 2 (actual + prepaid credit) |
| POP         | 1                | 0 (pay credit)              |
| MULTIPOP(k) | min(k,s)         | 0 (pay credit)              | 
### 2. Example of incrementing binary counter
| operations         | The actual costs | The amortized costs |
| ------------------ | ---------------- | ------------------- |
| BIT SET (0 -> 1)   | 1                | 2                   |
| BIT RESET (1 -> 0) | 1                | 0                   | 