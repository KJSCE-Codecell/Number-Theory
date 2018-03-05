# Euclid's Algorithm

Euclid's algorithm helps to find GCD of two numbers. Here's the psuedo code for it-
``` python
def euclidAlgo(a,b):
    if (a==0):
        return b
    else :
        return euclidAlgo(b%a,a)
```

**So, how does this work ?**
Basically, it writes b in terms of a, as -
b = a*⌊b/a⌋ + b%a, and passes the remainder, and divisor to next call, if the remainder is 0, we know that divisor is the GCD, if it isn't, it tries to find GCD between remainder and divisor, by writing divisor in terms of remainder, and goes on calling recursively, till remainder 0, then divisor is the GCD.

**Why find GCD of divisor and remainder?**
Since if divisor can be written in terms of remainder, then the dividend as whole can be written in terms of  remainder.

# Extended Euclid's Algorithm

It helps to find equation as -
ax + by = gcd(a,b)
and if this gcd is 1, it inturn can be used to find multiplicative inverse of a (mod b), or multiplicative inverse of b (mod a).

**What is multiplicative inverse ?**
In maths, as we know multiplicative inverse of any number a is 1/a since, multiplying both of them yields 1. 
Now, modulo multiplicative inverse is ax = 1 (mod b), is modulo multiplicative inverse of a under b. x here has to be among integers, so 1/a won't work.
Now, to find modulo multiplicative inverse using above - 
ax + by = gcd(a,b), if gcd(a,b)=1, **which is a necessary condition for finding modulo multiplicative inverse** can be wrote as -
ax + by = 1, now taking mod b, on both sides, a*(x mod b) + 0 = 1 (mod b), so here we have the answer !
Now, let's try to get it, dueing first call - 
```
As seen above, x and y are results for inputs a and b,
   a.x + b.y = gcd                      ----(1)  

And x1 and y1 are results for inputs b%a and a
   (b%a).x1 + a.y1 = gcd   
                    
When we put b%a = (b - (⌊b/a⌋).a) in above, 
we get following. Note that ⌊b/a⌋ is floor(a/b)

   (b - (⌊b/a⌋).a).x1 + a.y1  = gcd

Above equation can also be written as below
   b.x1 + a.(y1 - (⌊b/a⌋).x1) = gcd      ---(2)

After comparing coefficients of 'a' and 'b' in (1) and 
(2), we get following
   x = y1 - ⌊b/a⌋ * x1
   y = x1
```

Code for the same - 
``` python
def gcdExtended(a, b, x, y):

    if a == 0 : 
        x = 0
        y = 1
        return b
         
    x1 = 1
    y1 = 1
    gcd = gcdExtended(b%a, a, x1, y1)
 
    x = y1 - (b/a) * x1
    y = x1
 
    return gcd
```