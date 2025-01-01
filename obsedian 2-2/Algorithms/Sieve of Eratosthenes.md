#prime 

1. Create a list of consecutive integers from 2 through n: (2, 3, 4, ..., _n_).
2. Initially, let p equal 2, the smallest prime number.
3. Enumerate the multiples of p by counting in increments of p from 2_p_ to n, and mark them in the list (these will be 2_p_, 3_p_, 4_p_, ...; the p itself should not be marked).
4. Find the smallest number in the list greater than p that is not marked. If there was no such number, stop. Otherwise, let p now equal this new number (which is the next prime), and repeat from step 3.
5. When the algorithm terminates, the numbers remaining not marked in the list are all the primes below n.